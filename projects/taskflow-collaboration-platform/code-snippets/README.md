# 💻 Code Snippets

This folder contains important code examples and snippets from the TaskFlow Collaboration Platform. These examples demonstrate key implementation patterns, best practices, and reusable code components.

## 📁 Code Snippet Files

### Frontend Code Snippets

#### React Components
- **File**: `react-components.md`
- **Description**: Reusable React components with TypeScript
- **Examples**: TaskCard, ProjectBoard, UserAvatar, NotificationToast

#### State Management
- **File**: `state-management.md`
- **Description**: Zustand stores and React Query hooks
- **Examples**: useTaskStore, useProjectStore, useAuthStore

#### API Integration
- **File**: `api-integration.md`
- **Description**: API calls and data fetching patterns
- **Examples**: Task API, Project API, User API, File upload

#### Form Handling
- **File**: `form-handling.md`
- **Description**: React Hook Form with Zod validation
- **Examples**: Login form, Task creation, Project settings

### Backend Code Snippets

#### API Routes
- **File**: `api-routes.md`
- **Description**: Express.js API route handlers
- **Examples**: Auth routes, Task routes, Project routes, File routes

#### Database Operations
- **File**: `database-operations.md`
- **Description**: Prisma ORM queries and operations
- **Examples**: User queries, Task CRUD, Project management, Relations

#### Authentication
- **File**: `authentication.md`
- **Description**: JWT authentication and middleware
- **Examples**: Login logic, Token validation, Protected routes, Role-based access

#### Real-time Features
- **File**: `realtime-features.md`
- **Description**: Socket.io implementation
- **Examples**: Real-time updates, Live collaboration, Event handling

### Utility Functions

#### Common Utilities
- **File**: `utilities.md`
- **Description**: Reusable utility functions
- **Examples**: Date formatting, String manipulation, Validation helpers

#### API Helpers
- **File**: `api-helpers.md`
- **Description**: API utility functions
- **Examples**: Request helpers, Response formatting, Error handling

#### Database Helpers
- **File**: `database-helpers.md`
- **Description**: Database utility functions
- **Examples**: Query builders, Data transformers, Validation

## 🎯 Key Implementation Patterns

### 1. Component Architecture

#### TaskCard Component
```typescript
interface TaskCardProps {
  task: Task;
  onUpdate: (task: Task) => void;
  onDelete: (taskId: string) => void;
  isDragging?: boolean;
}

export const TaskCard: React.FC<TaskCardProps> = ({
  task,
  onUpdate,
  onDelete,
  isDragging = false
}) => {
  // Component implementation
};
```

#### Project Board Component
```typescript
interface ProjectBoardProps {
  project: Project;
  tasks: Task[];
  onTaskMove: (taskId: string, newStatus: TaskStatus) => void;
  onTaskCreate: (task: CreateTaskData) => void;
}

export const ProjectBoard: React.FC<ProjectBoardProps> = ({
  project,
  tasks,
  onTaskMove,
  onTaskCreate
}) => {
  // Board implementation with drag and drop
};
```

### 2. State Management Patterns

#### Zustand Store
```typescript
interface TaskStore {
  tasks: Task[];
  loading: boolean;
  error: string | null;
  fetchTasks: (projectId: string) => Promise<void>;
  createTask: (task: CreateTaskData) => Promise<void>;
  updateTask: (taskId: string, updates: Partial<Task>) => Promise<void>;
  deleteTask: (taskId: string) => Promise<void>;
}

export const useTaskStore = create<TaskStore>((set, get) => ({
  // Store implementation
}));
```

#### React Query Hooks
```typescript
export const useTasks = (projectId: string) => {
  return useQuery({
    queryKey: ['tasks', projectId],
    queryFn: () => taskApi.getTasks(projectId),
    staleTime: 5 * 60 * 1000, // 5 minutes
  });
};

export const useCreateTask = () => {
  const queryClient = useQueryClient();
  
  return useMutation({
    mutationFn: taskApi.createTask,
    onSuccess: (newTask) => {
      queryClient.invalidateQueries(['tasks', newTask.projectId]);
    },
  });
};
```

### 3. API Integration Patterns

#### API Client
```typescript
class TaskApiClient {
  private baseURL: string;
  
  constructor(baseURL: string) {
    this.baseURL = baseURL;
  }
  
  async getTasks(projectId: string): Promise<Task[]> {
    const response = await fetch(`${this.baseURL}/projects/${projectId}/tasks`);
    return response.json();
  }
  
  async createTask(task: CreateTaskData): Promise<Task> {
    const response = await fetch(`${this.baseURL}/tasks`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(task),
    });
    return response.json();
  }
}
```

#### Error Handling
```typescript
export const handleApiError = (error: unknown): string => {
  if (error instanceof Error) {
    return error.message;
  }
  
  if (typeof error === 'string') {
    return error;
  }
  
  return 'An unexpected error occurred';
};
```

### 4. Database Patterns

#### Prisma Models
```typescript
// User model
model User {
  id        String   @id @default(uuid())
  email     String   @unique
  firstName String
  lastName  String
  avatar    String?
  role      Role     @default(MEMBER)
  teams     TeamMember[]
  tasks     Task[]
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

// Task model
model Task {
  id          String     @id @default(uuid())
  title       String
  description String?
  status      TaskStatus @default(TODO)
  priority    Priority   @default(MEDIUM)
  dueDate     DateTime?
  project     Project    @relation(fields: [projectId], references: [id])
  projectId   String
  assignee    User?      @relation(fields: [assigneeId], references: [id])
  assigneeId  String?
  createdAt   DateTime   @default(now())
  updatedAt   DateTime   @updatedAt
}
```

#### Database Queries
```typescript
// Get tasks with relations
export const getTasksWithDetails = async (projectId: string) => {
  return await prisma.task.findMany({
    where: { projectId },
    include: {
      assignee: {
        select: { id: true, firstName: true, lastName: true, avatar: true }
      },
      project: {
        select: { id: true, name: true }
      }
    },
    orderBy: { createdAt: 'desc' }
  });
};

// Create task with validation
export const createTask = async (data: CreateTaskData) => {
  return await prisma.task.create({
    data: {
      title: data.title,
      description: data.description,
      projectId: data.projectId,
      assigneeId: data.assigneeId,
      dueDate: data.dueDate,
      priority: data.priority || 'MEDIUM'
    }
  });
};
```

### 5. Real-time Features

#### Socket.io Implementation
```typescript
// Server-side
io.on('connection', (socket) => {
  socket.on('join-project', (projectId: string) => {
    socket.join(`project-${projectId}`);
  });
  
  socket.on('task-updated', (data: TaskUpdateData) => {
    socket.to(`project-${data.projectId}`).emit('task-updated', data);
  });
});

// Client-side
export const useSocket = (projectId: string) => {
  const [socket, setSocket] = useState<Socket | null>(null);
  
  useEffect(() => {
    const newSocket = io(process.env.NEXT_PUBLIC_SOCKET_URL!);
    newSocket.emit('join-project', projectId);
    setSocket(newSocket);
    
    return () => {
      newSocket.disconnect();
    };
  }, [projectId]);
  
  return socket;
};
```

### 6. Form Handling

#### React Hook Form with Zod
```typescript
const taskSchema = z.object({
  title: z.string().min(1, 'Title is required'),
  description: z.string().optional(),
  assigneeId: z.string().optional(),
  dueDate: z.date().optional(),
  priority: z.enum(['LOW', 'MEDIUM', 'HIGH']).default('MEDIUM')
});

type TaskFormData = z.infer<typeof taskSchema>;

export const TaskForm: React.FC = () => {
  const { register, handleSubmit, formState: { errors } } = useForm<TaskFormData>({
    resolver: zodResolver(taskSchema)
  });
  
  const onSubmit = (data: TaskFormData) => {
    // Handle form submission
  };
  
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* Form fields */}
    </form>
  );
};
```

## 🔧 Utility Functions

### Date Utilities
```typescript
export const formatDate = (date: Date): string => {
  return new Intl.DateTimeFormat('en-US', {
    year: 'numeric',
    month: 'short',
    day: 'numeric'
  }).format(date);
};

export const isOverdue = (dueDate: Date): boolean => {
  return new Date() > dueDate;
};
```

### String Utilities
```typescript
export const truncateText = (text: string, maxLength: number): string => {
  if (text.length <= maxLength) return text;
  return text.substring(0, maxLength) + '...';
};

export const slugify = (text: string): string => {
  return text
    .toLowerCase()
    .replace(/[^\w\s-]/g, '')
    .replace(/[\s_-]+/g, '-')
    .replace(/^-+|-+$/g, '');
};
```

### Validation Utilities
```typescript
export const validateEmail = (email: string): boolean => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
};

export const validatePassword = (password: string): string[] => {
  const errors: string[] = [];
  
  if (password.length < 8) {
    errors.push('Password must be at least 8 characters long');
  }
  
  if (!/[A-Z]/.test(password)) {
    errors.push('Password must contain at least one uppercase letter');
  }
  
  if (!/[a-z]/.test(password)) {
    errors.push('Password must contain at least one lowercase letter');
  }
  
  if (!/\d/.test(password)) {
    errors.push('Password must contain at least one number');
  }
  
  return errors;
};
```

## 📚 Best Practices

### Code Organization
- Use TypeScript for type safety
- Implement proper error handling
- Follow consistent naming conventions
- Use meaningful variable and function names
- Add JSDoc comments for complex functions

### Performance Optimization
- Use React.memo for expensive components
- Implement proper dependency arrays in useEffect
- Use useCallback and useMemo appropriately
- Optimize database queries
- Implement proper caching strategies

### Security Considerations
- Validate all inputs on both client and server
- Use parameterized queries to prevent SQL injection
- Implement proper authentication and authorization
- Sanitize user-generated content
- Use HTTPS in production

### Testing Patterns
- Write unit tests for utility functions
- Test React components with React Testing Library
- Mock API calls in tests
- Test error scenarios
- Maintain good test coverage

---

**Note**: These code snippets serve as examples and should be adapted to your specific use case. Always follow your project's coding standards and best practices.
