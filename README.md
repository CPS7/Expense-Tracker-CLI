# Expense Tracker CLI
#### Video Demo:  https://youtu.be/Lc-Hwg0TP2w
#### Description:

Expense Tracker CLI is a robust Python-based command-line application designed to help users efficiently manage their personal finances. Tracking expenses is a universal problem, and this application provides a sleek, interactive terminal interface to record, categorize, and analyze spending behavior over time. The project is built leveraging modern Python libraries to deliver features like budget tracking, encrypted notes, and comprehensive data export capabilities including Excel and PDF reports with embedded charts.

## Project Architecture & Design Choices

When designing this application, the primary goal was to create a tool that is both feature-rich and easy to use directly from the terminal. A graphical user interface (GUI) was considered, but a CLI approach was chosen to ensure lightweight performance and ease of deployment across different environments. 

For the user interface, the `rich` library was selected over standard terminal printing. `rich` allows for beautiful, interactive elements like tables, panels, and styled prompts, which significantly elevates the user experience compared to plain text.

Data persistence is handled via SQLite. Instead of writing raw SQL queries, the SQLAlchemy Object-Relational Mapper (ORM) was utilized. This design choice provides a robust schema definition, simplifies database migrations, and protects against SQL injection vulnerabilities. The database schema encompasses several tables:
* `categories`: To store standard and user-defined expense categories.
* `expenses`: To log individual transactions, amounts, and dates.
* `budgets`: To track monthly spending limits per category.
* `expense_history`: To maintain an audit log of creation, updates, and soft deletions.

Security and privacy were also key considerations. Since financial data can be sensitive, an optional encryption feature was implemented using the `cryptography` library (specifically Fernet symmetric encryption) to encrypt transaction notes. This ensures that even if the database file is accessed by an unauthorized party, the contextual details of the expenses remain secure.

For data portability, the application supports exporting records to both Excel (`openpyxl`) and PDF (`fpdf`). A charting feature was integrated using `matplotlib` to visually represent spending trends, and these charts are automatically embedded into the generated PDF reports.

## File Descriptions

The project repository consists of the following key files:

* **`main.py`**: This is the core executable of the application. It contains the CLI routing logic, the SQLAlchemy database models, and the implementation of all primary features (adding expenses, viewing summaries, handling exports). The application loop and interactive menus are orchestrated from this file.
* **`test.py`**: Contains unit tests for the application to ensure that the core logic, such as budget calculation, encryption/decryption routines, and database interactions, function as expected. Testing is crucial to prevent regressions as new features are added.
* **`requirements.txt`**: Lists all the third-party Python packages required to run the application, including `rich`, `SQLAlchemy`, `fpdf`, `openpyxl`, `matplotlib`, and `cryptography`.
* **`.env.template`**: A template for the environment variables required to configure the application, specifically the encryption key (`EXPENSE_KEY`) and the toggle to enable/disable note encryption (`EXPENSE_ENCRYPT_NOTES`).
* **`README.md`**: This file, providing an overview of the project, setup instructions, and documentation required for the CS50 final project submission.

## Setup and Installation

1. Clone the repository to your local machine.
2. Create and activate a Python virtual environment to isolate dependencies.
3. Install the required packages using `pip install -r requirements.txt`.
4. (Optional) Copy `.env.template` to `.env` and configure your encryption key if you wish to use the secure notes feature.
5. Run the application using `python main.py` and follow the interactive prompts to start tracking your expenses.

By combining a functional ORM, a polished CLI interface, and practical data export options, the Expense Tracker CLI serves as a comprehensive tool for personal financial management and demonstrates a solid integration of various software engineering principles.
