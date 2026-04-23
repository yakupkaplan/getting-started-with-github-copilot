# Personal Notes

## Analyze new or unfamiliar code and how to generate documentation -> README Prompt

@workspace describe this project

I need a README file that includes the following sections:
Project Title: A brief, clear title for the project.
Description: A detailed explanation of what the project is and what it does.
Project Structure: A breakdown of the project structure, including key folders and files.
Key Classes and Interfaces: A list of key classes and interfaces in the project.
Usage: Instructions on how to use the project, often including code examples.
License: The license that the project is under.

## Developing new code featuers -> Commit messages and Pull Requests

Update the search_books method and ConsoleApp class so that when a user enters a book title, the app searches 
Books.json for a matching title (case-insensitive, partial match allowed). If a match is found, check all 
related BookItem records and their loan status in Loans.json. If any copy is not currently on loan (no active 
loan or has a ReturnDate), display "book.title is available for loan". If all copies are on loan, display 
"book.title is on loan to another patron. The return due date is loan.DueDate" (show the soonest due date). 
Integrate this logic into the user flow and ensure clear user messaging.


Update the ConsoleApp class and its search_books method to implement the following:

1. Add access to the loaded books data (from JsonData or a book repository) in ConsoleApp.
2. In search_books, use the user-supplied book title to search for a matching book in Books.json (case-insensitive, partial or exact match).
3. If a book is found, use its ID to find all related book items (copies) and check Loans.json to see if any copies are currently on loan (ReturnDate is null).
4. If at least one copy is available, display: "book.title is available for loan." If all are on loan, display: "book.title is on loan to another patron. The return due date is loan.DueDate."
5. If no book matches, inform the user. If multiple books match, prompt for refinement or selection.
6. After displaying the result, allow the user to search again or return to the previous menu.
    
Please provide the complete implementation for this book search and availability feature.

## Development of unit tests
    
Add new Pytest-style test functions to the following files: test_json_loan_repository.py, test_loan_service.py, and test_patron_service.py. 
- Do not remove or rewrite existing Unittest-based test classes or methods.
- Import pytest at the top if not already present.
- For each file, add:
    - At least one parameterized test using @pytest.mark.parametrize.
    - At least one fixture using @pytest.fixture for reusable setup.
    - At least one test using pytest.raises for exception/assertion testing.
- Name all new Pytest test functions with the test_ prefix.
- Clearly separate new Pytest functions from existing Unittest classes.
- If a fixture or parameterized test needs a dummy or mock class, define it within the file or reuse an existing one.
- Demonstrate how Pytest makes tests more concise and expressive compared to Unittest.

## Refactor existing code

@workspace Provide an explanation of how the current Python code can be improved with code refactoring to:
- avoid reflection
- avoid repeated `if/elif`
- make the code more explicit and efficient.
Then provide suggestion for refactoring this Python project to implement the improvement suggestions.


@workspace I need to refactor the `library\console\console_app.py` Python file to: Use dictionaries or switch expressions instead of reflection or long `if/elif` chains; Make mappings explicit for maintainability and efficiency; Use clear error handling for unknown cases; Provide refactored code to apply.

## Vibe Coding

I want to create a product requirements document (PRD) for an app that I'll develop using a vibe coding process. I want the PRD to include information about the app's purpose, target audience, features, and technical requirements. I've defined the following high-level parameters for my app: 
1 - Use HTML, CSS, and JavaScript to create a client-side web app. 
2 - Include the following web pages: Products, ProductDetails, ShoppingCart, and Checkout. 
3 - Enable navigation between pages. I want the prototype app to implement basic features and satisfy a small number of high-level use cases. 
The prototype should implement the following: basic use case functionality, simple navigation, a sample dataset, and basic styling. I'll be adding the PRD to the chat context, then asking GitHub Copilot Agent to create the prototype app. What sections should I include in the PRD to enable GitHub Copilot Agent to create my envisioned prototype?

The PRD sections that you suggested look good. Here's some information that should help you construct the PRD:

My prototype app targets online shoppers interested in ordering my products. The prototype should include the following:

- A dynamic user interface that scales automatically to appear correctly on large or small screens (desktop and phone devices).
- A simple dataset that defines 10 fruit products. The dataset should include: product name, description, price per unit (where unit could be the number of items, ounces, pounds, etc.). If possible, I want to include a simple image (an emoji) that represents the product.
- A navigation menu on the left side of the screen that allows users to navigate between the Products, ProductDetails, ShoppingCart, and Checkout pages.
- Basic styling that makes the user interface visually appealing, but it doesn't need to be fully responsive or polished.

The prototype app won't include any backend functionality, such as user authentication, payment processing, or database integration. It will be a static prototype that demonstrates the basic concepts.

Here's a description of the user interface:

- The Products page should display a list of products with basic information such as product name, price per unit, and an image (an emoji). The Products page should also provide a way to select a desired quantity of a product and an option to add selected items to the shopping cart.
- The ProductDetails page should display detailed information about a product when the product is selected from the Products page. The ProductDetails page should display the product name, a description of the product, the price per unit, and an image (an emoji) representing the product. The ProductDetails page should also provide a way to navigate back to the Products page.
- The ShoppingCart page should display the list of products added to the cart. The list should include the product name, quantity, and total price for that product. The ShoppingCart page should also provide a way to update the quantity of each product that's in the cart, and an option to remove products from the cart.
- The Checkout page should display a summary of the products being purchased, including product name, quantity, and price. The total price should be clearly displayed along with the option to "Process Order".
- The left-side navigation menu should provide basic navigation between pages. The navigation bar should collapse down to display a one or two letter abbreviation when the display width drops below 300 pixels. The navigation bar should allow users to navigate between the app pages.

## Consolidate duplicate code

@workspace Analyze the entire ECommerceOrderAndReturn codebase and identify all forms of code duplication, including method-level, service-level, and architectural pattern duplications. Prioritize the duplications by impact and refactoring difficulty. Describe an approach for consolidating this code.

## Refactor large functions

Create a detailed refactoring plan for the ProcessOrder method. Show me what the ProcessOrder method would look like after refactoring and provide a list of the methods that should be extracted. I'd like to keep the input validation and security checks together in a single method. Include suggestions for method signatures and return types that would maintain the current error handling behavior.

## Simplify complex conditionals

@workspace Analyze the CalculateFinalPrice method and suggest refactoring opportunities. Include options that move the nested conditional logic into more manageable, single-responsibility helper methods. Focus on the main discount paths: membership discounts, coupon discounts, and bulk discounts. Maintain the business logic while simplifying the code structure.

How can I simplify the complex conditional logic and reduce nesting levels in the CalculateFinalPrice method? For example, the method has multiple nested conditionals that apply different membership discounts based on user status and order details. What are some best practices for reducing nesting levels and improving readability? Explain the benefit of each approach when applied to the CalculateFinalPrice method.

## Implement performance profiling

Analyze the ProductCatalog class for performance bottlenecks. Focus on the GetProductById, SearchProducts, and GetProductsByCategory methods. What are the main inefficiencies and how could they be optimized?

Examine the OrderProcessor class, particularly the CalculateOrderTotal and FinalizeOrderAsync methods. What performance problems do you see and what optimization strategies would you recommend?

Do any of the suggested optimizations include security risks or introduce other adverse effects?

## Resolve GitHub issues

Analyze the SearchProducts method for SQL injection vulnerabilities. Consider the following issue description: "The product search functionality is vulnerable to SQL injection attacks. User input is directly concatenated into SQL queries without proper parameterization or sanitization." Explain the impact of directly concatenating user input into SQL queries without proper parameterization or sanitization. What are the potential consequences if an attacker exploits this vulnerability?

#codebase I need to resolve SQL injection vulnerabilities associated with the SearchProducts method in the ProductService.cs file. Notice that user input is directly concatenated into SQL queries without proper parameterization or sanitization. The updated codebase should use parameterized queries or prepared statements, implement proper input validation and sanitization, remove debug logging of SQL queries, and add input length restrictions. My acceptance criteria includes: User input is properly parameterized; No raw SQL construction with user input; Input validation prevents malicious characters; Debug logging removed or sanitized. Review the codebase and identify the code files that must be updated to address the SQL injection vulnerability. Based on your code review and the current Chat conversation, suggest a phased approach to required file updates.

## Configure GitHub Copilot instructions and create custom agents

Contoso Inventory API - Coding Standards

Naming Conventions
- Use PascalCase for class names, public methods, and public properties.
- Use camelCase for local variables and method parameters.
- Prefix private fields with an underscore (e.g., _inventoryService).
- Suffix interface names with the interface prefix "I" (e.g., IInventoryService).

Architecture Patterns
- Follow the repository pattern for all data access operations.
- Use dependency injection for all service dependencies. Register services in Program.cs.
- Separate business logic into service classes. Controllers should only handle HTTP concerns.
- Use DTOs (Data Transfer Objects) for API request and response payloads. Never expose database entities directly.

Error Handling
- Use try-catch blocks for all external API calls and database operations.
- Return appropriate HTTP status codes (200 for success, 400 for bad requests, 404 for not found, 500 for server errors).
- Log all exceptions using ILogger<T> with structured logging.
- Include meaningful error messages in API responses.

Documentation
- Include XML documentation comments on all public methods and classes.
- Use inline comments only for complex business logic that is not self-explanatory.

Testing
- Write unit tests using xUnit and Moq.
- Follow the Arrange-Act-Assert pattern in test methods.
- Name test methods using the pattern: MethodName_Scenario_ExpectedResult.

etc.

## Agent Example

 ---
 description: Analyzes feature requirements and generates implementation plans without writing code
 tools: ['search', 'read', 'fetch']
 handoffs:
   - label: Start Implementation
     agent: implementer
     prompt: "Implement the plan outlined above. Follow the project's custom instructions for coding standards. Create all necessary files including models, DTOs, services, interfaces, and controllers."
     send: false
   - label: Write Tests First
     agent: implementer
     prompt: "Before implementing the feature, write unit tests based on the plan outlined above. Use xUnit and Moq following the project's testing conventions. Create test classes that cover the service methods and controller actions described in the plan. Do not implement the production code yet—only the tests."
     send: false
 ---
 # Planner

 You are a senior software architect working on a C# ASP.NET Core Web API project. When the user describes a feature or change, analyze the request and generate a detailed implementation plan.

 Before creating a plan, always search the existing codebase to understand the current project structure, coding patterns, and dependencies already in place.

 Your plan MUST include:
 1. **Summary**: A brief overview of the feature and its purpose.
 2. **Files to create or modify**: A complete list of files that need to be created or changed, with their full paths.
 3. **Implementation steps**: Step-by-step tasks in logical dependency order. Each step should specify what to do and which file to work in.
 4. **Models and DTOs**: Define the data structures needed, including property names and types.
 5. **Service interface and implementation**: Outline the service methods needed and their signatures.
 6. **Controller endpoints**: List the API endpoints to create, including HTTP methods, routes, request/response types, and status codes.
 7. **Dependency injection**: Specify any service registrations needed in Program.cs.
 8. **Risks and considerations**: Highlight potential issues, edge cases, or decisions that need input.

 IMPORTANT RULES:
 - Do NOT write or modify any code. Focus on planning only.
 - Do NOT create files. Your role is advisory.
 - Follow the project's established architecture patterns and coding standards.
 - Ask clarifying questions if the requirements are ambiguous.
 - Reference existing code patterns in the project for consistency.


  Analyze the project structure and describe the current architecture, including any existing models, services, and controllers. Identify the patterns used in the Category feature implementation.