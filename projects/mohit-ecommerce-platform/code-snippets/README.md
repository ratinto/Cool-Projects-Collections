# 💻 Code Snippets

This folder contains important code examples and snippets from the Mohit E-Commerce Platform.

## Frontend Code Examples

### React Components

#### ProductCard Component
```tsx
// components/ProductCard.tsx
import React from 'react';
import { Product } from '../types/product';
import { useAppDispatch } from '../hooks/redux';
import { addToCart } from '../store/slices/cartSlice';

interface ProductCardProps {
  product: Product;
}

const ProductCard: React.FC<ProductCardProps> = ({ product }) => {
  const dispatch = useAppDispatch();

  const handleAddToCart = () => {
    dispatch(addToCart({
      id: product._id,
      name: product.name,
      price: product.price,
      image: product.images[0],
      quantity: 1
    }));
  };

  return (
    <div className="bg-white rounded-lg shadow-md overflow-hidden hover:shadow-lg transition-shadow">
      <img 
        src={product.images[0]} 
        alt={product.name}
        className="w-full h-48 object-cover"
      />
      <div className="p-4">
        <h3 className="text-lg font-semibold text-gray-800">{product.name}</h3>
        <p className="text-gray-600 text-sm mt-1">{product.description}</p>
        <div className="flex items-center justify-between mt-3">
          <span className="text-xl font-bold text-green-600">
            ${product.price}
          </span>
          <button 
            onClick={handleAddToCart}
            className="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700"
          >
            Add to Cart
          </button>
        </div>
      </div>
    </div>
  );
};

export default ProductCard;
```

#### Custom Hook for API Calls
```tsx
// hooks/useProducts.ts
import { useState, useEffect } from 'react';
import { Product } from '../types/product';
import { apiClient } from '../utils/apiClient';

export const useProducts = (category?: string) => {
  const [products, setProducts] = useState<Product[]>([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    const fetchProducts = async () => {
      try {
        setLoading(true);
        const response = await apiClient.get('/products', {
          params: { category }
        });
        setProducts(response.data.products);
      } catch (err) {
        setError('Failed to fetch products');
        console.error(err);
      } finally {
        setLoading(false);
      }
    };

    fetchProducts();
  }, [category]);

  return { products, loading, error };
};
```

#### Redux Store Configuration
```tsx
// store/index.ts
import { configureStore } from '@reduxjs/toolkit';
import { setupListeners } from '@reduxjs/toolkit/query';
import authSlice from './slices/authSlice';
import cartSlice from './slices/cartSlice';
import { productApi } from './api/productApi';

export const store = configureStore({
  reducer: {
    auth: authSlice,
    cart: cartSlice,
    [productApi.reducerPath]: productApi.reducer,
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware({
      serializableCheck: {
        ignoredActions: ['persist/PERSIST'],
      },
    }).concat(productApi.middleware),
});

setupListeners(store.dispatch);

export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
```

## Backend Code Examples

### Express.js Route Handlers

#### Product Routes
```typescript
// routes/productRoutes.ts
import express from 'express';
import { 
  getProducts, 
  getProductById, 
  createProduct, 
  updateProduct, 
  deleteProduct 
} from '../controllers/productController';
import { auth, adminAuth } from '../middleware/auth';
import { validateProduct } from '../middleware/validation';
import { upload } from '../middleware/upload';

const router = express.Router();

// Public routes
router.get('/', getProducts);
router.get('/:id', getProductById);

// Admin routes
router.post('/', auth, adminAuth, upload.array('images', 5), validateProduct, createProduct);
router.put('/:id', auth, adminAuth, upload.array('images', 5), validateProduct, updateProduct);
router.delete('/:id', auth, adminAuth, deleteProduct);

export default router;
```

#### Product Controller
```typescript
// controllers/productController.ts
import { Request, Response } from 'express';
import Product from '../models/Product';
import { cloudinary } from '../utils/cloudinary';
import { ApiError } from '../utils/ApiError';

export const getProducts = async (req: Request, res: Response) => {
  try {
    const page = parseInt(req.query.page as string) || 1;
    const limit = parseInt(req.query.limit as string) || 12;
    const category = req.query.category as string;
    const search = req.query.search as string;

    const filter: any = {};
    if (category) filter.category = category;
    if (search) {
      filter.$or = [
        { name: { $regex: search, $options: 'i' } },
        { description: { $regex: search, $options: 'i' } }
      ];
    }

    const products = await Product.find(filter)
      .populate('category')
      .sort({ createdAt: -1 })
      .limit(limit * 1)
      .skip((page - 1) * limit);

    const total = await Product.countDocuments(filter);

    res.json({
      products,
      totalPages: Math.ceil(total / limit),
      currentPage: page,
      total
    });
  } catch (error) {
    res.status(500).json({ message: 'Server error', error: error.message });
  }
};

export const createProduct = async (req: Request, res: Response) => {
  try {
    const { name, description, price, category, brand, stock } = req.body;
    const files = req.files as Express.Multer.File[];

    // Upload images to Cloudinary
    const imageUrls = await Promise.all(
      files.map(async (file) => {
        const result = await cloudinary.uploader.upload(file.path, {
          folder: 'ecommerce/products',
          transformation: [
            { width: 800, height: 600, crop: 'fill' },
            { quality: 'auto' }
          ]
        });
        return result.secure_url;
      })
    );

    const product = new Product({
      name,
      description,
      price,
      category,
      brand,
      stock,
      images: imageUrls,
      sku: generateSKU(name, brand)
    });

    await product.save();
    await product.populate('category');

    res.status(201).json({
      message: 'Product created successfully',
      product
    });
  } catch (error) {
    res.status(400).json({ message: 'Error creating product', error: error.message });
  }
};
```

### Database Models

#### Product Model (Mongoose)
```typescript
// models/Product.ts
import mongoose, { Document, Schema } from 'mongoose';

export interface IProduct extends Document {
  name: string;
  description: string;
  price: number;
  discountPrice?: number;
  category: mongoose.Types.ObjectId;
  brand: string;
  images: string[];
  stock: number;
  sku: string;
  ratings: {
    average: number;
    count: number;
  };
  specifications: Map<string, string>;
  tags: string[];
  isActive: boolean;
  createdAt: Date;
  updatedAt: Date;
}

const productSchema = new Schema<IProduct>({
  name: {
    type: String,
    required: true,
    trim: true,
    index: true
  },
  description: {
    type: String,
    required: true
  },
  price: {
    type: Number,
    required: true,
    min: 0
  },
  discountPrice: {
    type: Number,
    min: 0
  },
  category: {
    type: Schema.Types.ObjectId,
    ref: 'Category',
    required: true
  },
  brand: {
    type: String,
    required: true
  },
  images: [{
    type: String,
    required: true
  }],
  stock: {
    type: Number,
    required: true,
    min: 0
  },
  sku: {
    type: String,
    required: true,
    unique: true
  },
  ratings: {
    average: {
      type: Number,
      default: 0,
      min: 0,
      max: 5
    },
    count: {
      type: Number,
      default: 0
    }
  },
  specifications: {
    type: Map,
    of: String
  },
  tags: [{
    type: String,
    index: true
  }],
  isActive: {
    type: Boolean,
    default: true
  }
}, {
  timestamps: true
});

// Indexes for better query performance
productSchema.index({ name: 'text', description: 'text' });
productSchema.index({ category: 1, price: 1 });
productSchema.index({ tags: 1 });

export default mongoose.model<IProduct>('Product', productSchema);
```

### Authentication Middleware
```typescript
// middleware/auth.ts
import { Request, Response, NextFunction } from 'express';
import jwt from 'jsonwebtoken';
import User from '../models/User';

interface AuthRequest extends Request {
  user?: any;
}

export const auth = async (req: AuthRequest, res: Response, next: NextFunction) => {
  try {
    const token = req.header('Authorization')?.replace('Bearer ', '');
    
    if (!token) {
      return res.status(401).json({ message: 'No token, authorization denied' });
    }

    const decoded = jwt.verify(token, process.env.JWT_SECRET!) as any;
    const user = await User.findById(decoded.userId).select('-password');
    
    if (!user) {
      return res.status(401).json({ message: 'Token is not valid' });
    }

    req.user = user;
    next();
  } catch (error) {
    res.status(401).json({ message: 'Token is not valid' });
  }
};

export const adminAuth = (req: AuthRequest, res: Response, next: NextFunction) => {
  if (req.user && req.user.role === 'admin') {
    next();
  } else {
    res.status(403).json({ message: 'Admin access required' });
  }
};
```

## Utility Functions

### API Client (Axios Configuration)
```typescript
// utils/apiClient.ts
import axios from 'axios';
import { store } from '../store';
import { logout } from '../store/slices/authSlice';

const apiClient = axios.create({
  baseURL: process.env.REACT_APP_API_URL || 'http://localhost:5000/api',
  timeout: 10000,
});

// Request interceptor
apiClient.interceptors.request.use(
  (config) => {
    const token = store.getState().auth.token;
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);

// Response interceptor
apiClient.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      store.dispatch(logout());
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);

export { apiClient };
```

### Image Upload Utility
```typescript
// utils/cloudinary.ts
import { v2 as cloudinary } from 'cloudinary';
import { CloudinaryStorage } from 'multer-storage-cloudinary';
import multer from 'multer';

cloudinary.config({
  cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
  api_key: process.env.CLOUDINARY_API_KEY,
  api_secret: process.env.CLOUDINARY_API_SECRET,
});

const storage = new CloudinaryStorage({
  cloudinary: cloudinary,
  params: {
    folder: 'ecommerce',
    allowed_formats: ['jpg', 'jpeg', 'png', 'webp'],
    transformation: [{ width: 1000, height: 1000, crop: 'limit' }],
  } as any,
});

export const upload = multer({ storage });
export { cloudinary };
```

## Docker Configuration

### Dockerfile (Frontend)
```dockerfile
# frontend/Dockerfile
FROM node:18-alpine as builder

WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### Docker Compose
```yaml
# docker-compose.yml
version: '3.8'

services:
  frontend:
    build: ./frontend
    ports:
      - "3000:80"
    environment:
      - REACT_APP_API_URL=http://localhost:5000/api
    depends_on:
      - backend

  backend:
    build: ./backend
    ports:
      - "5000:5000"
    environment:
      - NODE_ENV=development
      - MONGODB_URI=mongodb://mongo:27017/ecommerce
      - JWT_SECRET=your-secret-key
    depends_on:
      - mongo
    volumes:
      - ./backend:/app
      - /app/node_modules

  mongo:
    image: mongo:6.0
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

## Testing Examples

### React Component Test
```typescript
// __tests__/ProductCard.test.tsx
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import { Provider } from 'react-redux';
import { store } from '../store';
import ProductCard from '../components/ProductCard';

const mockProduct = {
  _id: '1',
  name: 'Test Product',
  description: 'Test Description',
  price: 99.99,
  images: ['test-image.jpg'],
  category: 'electronics',
  brand: 'TestBrand',
  stock: 10
};

const renderWithProvider = (component: React.ReactElement) => {
  return render(
    <Provider store={store}>
      {component}
    </Provider>
  );
};

describe('ProductCard', () => {
  test('renders product information correctly', () => {
    renderWithProvider(<ProductCard product={mockProduct} />);
    
    expect(screen.getByText('Test Product')).toBeInTheDocument();
    expect(screen.getByText('Test Description')).toBeInTheDocument();
    expect(screen.getByText('$99.99')).toBeInTheDocument();
  });

  test('adds product to cart when button is clicked', () => {
    renderWithProvider(<ProductCard product={mockProduct} />);
    
    const addToCartButton = screen.getByText('Add to Cart');
    fireEvent.click(addToCartButton);
    
    // Add assertions based on your cart implementation
  });
});
```

### API Endpoint Test
```typescript
// __tests__/productRoutes.test.ts
import request from 'supertest';
import app from '../app';
import Product from '../models/Product';

describe('Product Routes', () => {
  beforeEach(async () => {
    await Product.deleteMany({});
  });

  describe('GET /api/products', () => {
    test('should return all products', async () => {
      const response = await request(app)
        .get('/api/products')
        .expect(200);

      expect(response.body).toHaveProperty('products');
      expect(Array.isArray(response.body.products)).toBe(true);
    });

    test('should filter products by category', async () => {
      const response = await request(app)
        .get('/api/products?category=electronics')
        .expect(200);

      expect(response.body.products).toEqual(
        expect.arrayContaining([
          expect.objectContaining({
            category: expect.objectContaining({
              name: 'electronics'
            })
          })
        ])
      );
    });
  });
});
```

---

These code snippets provide practical examples of how to implement key features in a full-stack e-commerce application using modern technologies and best practices.
