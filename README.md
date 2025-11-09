##  SAS Enterprise Guide Process Flow Automation

##[Code Compilation](https://github.com/harrybehn/PortfolioProjectCode/blob/main/Program%20Email%20sending.sas)

This project showcases a complete automated process flow built in SAS Enterprise Guide (EG). It demonstrates how to manage ETL, transform data, generate reports, and automate email delivery using native SAS capabilities and Windows Task Scheduler.

---

## ETL Process
- Uses PROC SQL to join and transform data from multiple source tables: GAMINGSESSION, PLAYER, and NATIONALITY.
- Performs a LEFT JOIN to enrich session data with player nationality.
- Derives new fields:
  - GameType: Categorizes sessions as Table, Slot, or ETG based on GamingArea1.
  - Period: Maps specific EndTime dates to reporting periods like Yesterday, P1W, P2W, etc.
  - NationalityGroup: Groups players into Philippines, USA, or Others based on nationality.
- Outputs a cleaned and enriched dataset MERGED_TABLES for downstream processing.

## Transpose using a Program
- Uses PROC TRANSPOSE to reshape the dataset work.R1 into work.R2.
- Groups data by NationalityGroup using the BY statement.
- Pivots the values of UniquePlayer, CoinIn, ActualWin, and TheoWin across different Period values using the ID statement.
- This transformation converts long-format data into wide-format, making it easier to compare metrics across time periods for each nationality group.

## Automated Report Generation
- Configures SAS to send emails via SMTP using the emailhost and emailsys options.
- Uses FILENAME msg EMAIL to define the email recipient, sender, subject, and content type (text/html).
- Embeds a styled HTML message using ODS HTML and escape characters for formatting.
- Generates a detailed report using PROC REPORT:
  - Summarizes gaming performance by Category and NationalityGroup.
  - Compares metrics across periods (Yesterday, P1W, P2W, P3W) and calculates percentage differences.
  - Applies formatting for readability (e.g., bold headers, percent formats).
- Appends a closing message and sends the report as an HTML email.


