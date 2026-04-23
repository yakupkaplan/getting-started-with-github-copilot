# Library Management System

## Project Title

**Library Management System** - A comprehensive library management application for handling patron accounts, book loans, and membership renewals.

## Description

The Library Management System is a Python-based application designed to manage library operations efficiently. It provides functionality for:

- **Patron Management**: Register and manage library patrons, track membership status, and handle membership renewals
- **Loan Management**: Track book loans, manage due dates, extend loans, and process book returns
- **Book Inventory**: Maintain a catalog of books and book items with condition tracking
- **Membership Renewal**: Automated membership renewal with validation checks
- **Data Persistence**: JSON-based data storage for patrons, loans, and books

The application features a command-line interface that allows library staff to interact with the system and perform daily operations.

## Project Structure

```
library/
├── application_core/
│   ├── entities/
│   │   ├── book.py                  # Book entity
│   │   ├── book_item.py             # Individual book copy entity
│   │   ├── loan.py                  # Loan entity for book borrowing
│   │   └── patron.py                # Library patron entity
│   ├── interfaces/
│   │   ├── iloan_repository.py      # Loan repository interface
│   │   ├── iloan_service.py         # Loan service interface
│   │   ├── ipatron_repository.py    # Patron repository interface
│   │   └── ipatron_service.py       # Patron service interface
│   ├── services/
│   │   ├── loan_service.py          # Loan business logic
│   │   └── patron_service.py        # Patron business logic
│   └── enums/
│       ├── loan_extension_status.py # Loan extension status enum
│       ├── loan_return_status.py    # Loan return status enum
│       └── membership_renewal_status.py  # Membership renewal status enum
├── infrastructure/
│   ├── json_data.py                 # JSON data storage handler
│   ├── json_loan_repository.py      # Loan repository implementation
│   ├── json_patron_repository.py    # Patron repository implementation
│   └── json_book_repository.py      # Book repository implementation
├── console/
│   ├── main.py                      # Application entry point
│   ├── console_app.py               # Console application controller
│   ├── console_state.py             # Console state management
│   └── common_actions.py            # Common console actions
├── tests/
│   ├── test_patron_service.py       # Patron service unit tests
│   └── test_loan_service.py         # Loan service unit tests
└── README.md                        # This file
```

### Key Directories

- **application_core/**: Contains the core business logic, including entities, services, and interfaces following domain-driven design principles
- **infrastructure/**: Handles data persistence using JSON files
- **console/**: Provides a command-line interface for user interaction
- **tests/**: Contains unit tests for the services

## Key Classes and Interfaces

### Entities

- **Patron**: Represents a library patron with membership information
  - Properties: `id`, `name`, `membership_start`, `membership_end`, `image_name`, `loans`

- **Loan**: Represents a book loan transaction
  - Properties: `id`, `book_item_id`, `patron_id`, `loan_date`, `due_date`, `return_date`, `book_item`, `patron`

- **BookItem**: Represents an individual copy of a book
  - Properties: `id`, `book_id`, `acquisition_date`, `condition`, `book`

- **Book**: Represents a book in the library catalog
  - Properties: `id`, `title`, `author`, `isbn`, `publication_date`

### Interfaces

- **IPatronService**: Interface for patron business logic
  - Method: `renew_membership(patron_id: int) -> MembershipRenewalStatus`

- **ILoanService**: Interface for loan business logic
  - Methods:
    - `return_loan(loan_id: int) -> LoanReturnStatus`
    - `extend_loan(loan_id: int) -> LoanExtensionStatus`

- **IPatronRepository**: Interface for patron data access
  - Methods: `get_patron()`, `add_patron()`, `update_patron()`, etc.

- **ILoanRepository**: Interface for loan data access
  - Methods: `get_loan()`, `add_loan()`, `update_loan()`, etc.

### Services

- **PatronService**: Handles patron operations including membership renewal with validation
- **LoanService**: Manages loan operations including returns and extensions

### Status Enums

- **MembershipRenewalStatus**: `SUCCESS`, `PATRON_NOT_FOUND`, `TOO_EARLY_TO_RENEW`, `LOAN_NOT_RETURNED`, `ERROR`
- **LoanReturnStatus**: `SUCCESS`, `LOAN_NOT_FOUND`, `ALREADY_RETURNED`, `ERROR`
- **LoanExtensionStatus**: `SUCCESS`, `LOAN_NOT_FOUND`, `OVERDUE`, `ALREADY_EXTENDED`, `ERROR`

## Usage

### Installation

1. Ensure you have Python 3.11+ installed
2. Install dependencies using uv:

   ```bash
   uv sync
   ```

### Running the Application

From the project root directory:

```bash
uv run python library/console/main.py
```

Or with auto-reload:

```bash
uv run --watch python library/console/main.py
```

### Console Interface

Once the application starts, you'll have access to a menu-driven interface with options to:

- View patron information
- Manage book loans (borrow, return, extend)
- Renew memberships
- View library inventory
- Check loan history

### Programmatic Usage

#### Creating a Patron Service

```python
from library.application_core.services.patron_service import PatronService
from library.infrastructure.json_patron_repository import JsonPatronRepository
from library.infrastructure.json_data import JsonData

# Initialize data and repository
json_data = JsonData()
patron_repo = JsonPatronRepository(json_data)

# Create service
patron_service = PatronService(patron_repo)

# Renew a patron's membership
status = patron_service.renew_membership(patron_id=1)
print(status.value)
```

#### Creating a Loan Service

```python
from library.application_core.services.loan_service import LoanService
from library.infrastructure.json_loan_repository import JsonLoanRepository

# Initialize repository and service
json_data = JsonData()
loan_repo = JsonLoanRepository(json_data)
loan_service = LoanService(loan_repo)

# Return a book
status = loan_service.return_loan(loan_id=1)
print(status.value)

# Extend a loan
status = loan_service.extend_loan(loan_id=1)
print(status.value)
```

### Running Tests

Execute the test suite:

```bash
uv run pytest library/tests/
```

Run tests with coverage:

```bash
uv run pytest library/tests/ --cov=library
```

## License

This project is licensed under the MIT License - see the [LICENSE](../LICENSE) file in the project root for details.
