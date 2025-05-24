# AI Bill Application

A Java-based personal finance management system with AI-powered spending analysis and visualization capabilities.

## Features

-  Transaction management (CRUD operations)
-  Financial statistics and visualizations (histograms, monthly summaries)
-  AI-driven spending pattern analysis 
-  User authentication and role-based access
-  CSV-based data persistence
-  Caching system for performance optimization
-  Comprehensive unit test coverage

## Technologies

- **Core**: Java 21
- **Build**: Maven
- **AI Integration**: DeepSeek API
- **UI**: Java Swing
- **Testing**: JUnit 5
- **Caching**: Caffeine

## Installation

1. Clone repository:
   ```bash
   git clone https://github.com/yourusername/Ai-Bill-Application.git
   ```
## Configuration

1. Create `config.properties` in `src/main/resources`:
   ```properties
   # DeepSeek API Configuration
    setx VOLCENGINE_ACCESS_KEY AKLTN2ZiY2Q4ODBhOWM3NDE4MzgzYjliZmNiMjQ0ZWJmMDQ
    setx VOLCENGINE_SECRET_KEY T0RkaFpUVXhZV1JrTUdObE5EVmlNMkUzT0RRellXUTRNekJrTXpNeVl6WQ==
    setx ARK_API_KEY fbd792bd-8463-4063-89d9-2d4b5bd7ef13
   # CSV Storage Paths
   csv.users.path=CSVForm/users/users.csv
   csv.transactions.dir=CSVForm/transactions
   csv.stats.dir=CSVForm/stats
   ```


Key Functionality:
-  User registration/login
-  Add transactions with categories
-  View monthly spending summaries
-  Generate spending pattern visualizations
-  Get AI-generated financial advice

## Code Structure and Key Classes

### Core Components

#### Controller Package
- **UserDialog**: Handles user authentication flows 
  - `void showLoginDialog()`: Displays modal dialog with login/registration form
  - `boolean validateCredentials(String username, String password)`: Verifies credentials against user CSV
  
- **MenuUI**: Manages main application interface
  - `JMenuBar initializeMenuBar()`: Constructs Swing menu with Data/Analysis/Help tabs
  - `void showTransactionTable(List<Transaction>)`: Displays paginated records with sorting

#### DAO Package
- **CsvTransactionDao**: (Implements TransactionDao)
  - `void saveTransaction(Transaction t)`: Persists to user-specific CSV with ISO date formatting
  - `List<Transaction> findByDateRange(LocalDate start, LocalDate end)`: Retrieves using Java Time API

#### Service Package
- **TransactionServiceImpl**: (Implements TransactionService)
  - `Map<Category, BigDecimal> analyzeSpendingPatterns()`: Groups by category with monetary sums
  - `String generateAIRecommendations(String prompt)`: Uses DeepSeek API with prompt templating

- **AIAnalyzerThread**: Background AI processing
  - `void run()`: Implements Runnable for concurrent analysis
  - `BudgetPlan generateBudgetPlan(User user)`: Creates with 50/30/20 rule implementation

#### Model Package
- **Transaction**: Core domain object
  - `String toCSV()`: Produces comma-separated: date,amount,category,description
  - `void validateAmount()`: Throws IllegalArgumentException for negative values
  
- **User**: Manages account details
  - `void hashPassword()`: Uses BCrypt with 10 rounds salt
  - `boolean hasAdminRole()`: Checks "isAdmin" flag in CSV record

### Utility Classes
- **CacheManager**: Optimizes data access
  - `Cache<String, List<Transaction>> getCaffeineCache()`: 1MB max, 5min expiry
  - `void refreshCache(String username)`: Evicts cache entries on data changes

- **CollegeStudentNeeds**: AI personality profile
  - `List<Transaction> generateMockSpending(int months)`: Creates textbook/rent/food patterns
  - `Map<String, BigDecimal> analyzeEssentialSpending()`: Flags non-academic expenses

## Project Structure

```
src/
├── main
│   ├── java
│   │   └── com
│   │       └── group21
│   │           └── ai
│   │               ├── Controller      # UI Components
│   │               ├── DAO            # Data Access Objects
│   │               ├── Service         # Business Logic
│   │               ├── model           # Domain Models
│   │               └── Utils          # Utility Classes
│   └── resources
│       └── CSVForm                   # CSV Storage
└── test
    └── java                         # Unit Tests
```

## Contributing

1. Fork the repository
2. Create feature branch:
   ```bash
   git checkout -b feature/new-feature
   ```
3. Write tests for new functionality
4. Submit pull request
