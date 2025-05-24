*   **AI-Powered Financial Analysis:**
    *   **General Transaction Analysis:** Users can input natural language requests, and AI analyzes raw transaction data within a specified time range.
    *   **Personal Spending Summary:** AI generates a summary of personal spending habits based on monthly aggregated data.
    *   **Savings Goal Suggestions:** AI provides savings goal suggestions based on monthly income and expenditure.
    *   **Personalized Saving Tips:** AI offers targeted saving tips based on monthly spending categories.
    *   **Student-Specific Advice:**
        *   Budget suggestions for students.
        *   Saving tips tailored for students.
    *   **AI Category Recognition:** AI assists in suggesting transaction categories when adding or modifying transactions.
    *   **[New Feature] Localized Financial Context Analysis (China Focus):**
        *   Analyzes users' seasonal spending patterns in China.
        *   Pays special attention to spending changes and trends during major Chinese public holidays (e.g., Spring Festival, National Day).
        *   Analyzes expenses related to clothing, etc., during seasonal changes (e.g., spring/summer, autumn/winter transitions).
        *   Identifies unusual spending behavior inconsistent with seasonal characteristics.
        *   Provides targeted budgeting advice and financial planning tips.
*   **Admin Statistics:**
    *   Generates and displays weekly summary statistics for all users (total income, total expenses, top spending categories, etc.).

## Technology Stack

*   **Backend:** Java
*   **AI Model API:** Volcengine Ark - (Please confirm the specific model, e.g., `ep-20250308174053-7pbkq`)
*   **GUI:** Java Swing, FlatLaf (for look and feel)
*   **Data Storage:** CSV files
*   **Charting Library:** XChart
*   **CSV Handling:** Apache Commons CSV
*   **Caching:** Caffeine
*   **Build Tool:** (e.g., Maven, Gradle - Please specify for your project)

## New AI Feature: Localized Financial Context Analysis

This branch introduces a new AI analysis feature designed to provide financial insights more relevant to users in China.

**Feature Highlights:**

1.  **Chinese Public Holiday Spending Analysis:**
    *   The AI specifically analyzes spending patterns around major Chinese public holidays: Spring Festival (Chinese New Year), Qingming Festival, Labor Day, Dragon Boat Festival (Duanwu), National Day, and New Year's Day.
    *   Identifies significant increases or changes in spending categories such as travel, gifts, dining out, and red packets (hongbao) during these periods.
    *   Provides budgeting advice to prepare for these holidays based on past spending.

2.  **Seasonal Spending & Budgeting:**
    *   Analyzes spending on clothing during seasonal changes (e.g., spring/summer, autumn/winter transitions).
    *   Suggests budgets for seasonal wardrobe updates.
    *   Attempts to identify spending patterns inconsistent with the current season in China (e.g., high spending on winter clothing in summer).

**Implementation Details:**

*   This feature is primarily implemented by enhancing Prompt Engineering within `AITransactionService.java`.
*   The AI analysis is based on the user's monthly summary bill data (`MonthlySummary`).
*   By providing the AI model with more detailed instructions that include China-specific cultural and seasonal factors, it's guided to generate more localized insights.
*   A new button, "Analyze Seasonal Spending (China Focus)," has been added to the AI analysis panel in `MenuUI.java` to trigger this function.
