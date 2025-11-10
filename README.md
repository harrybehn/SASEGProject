##  SAS Enterprise Guide Process Flow Automation

[See Code here](https://github.com/harrybehn/PortfolioProjectCode/blob/main/Program%20Email%20sending.sas)

This project showcases a complete automated process flow built in SAS Enterprise Guide (EG). It demonstrates how to manage ETL, transform data, generate reports, and automate email delivery using native SAS capabilities and Windows Task Scheduler.

---

## ETL Process
- Join and transform data from multiple source tables: GAMINGSESSION, PLAYER, and NATIONALITY.
- Performs a LEFT JOIN to add the player nationality in GamingSession table.
- Creates Computed Columns:
  - GameType: Categorizes sessions as Table, Slot, or ETG based on GamingArea1.
  - Period: Maps specific EndTime dates to reporting periods like Yesterday, P1W, P2W, etc.
  - NationalityGroup: Groups players into Philippines, USA, or Others based on nationality.
<img width="1160" height="737" alt="Image" src="https://github.com/user-attachments/assets/13845f77-2d53-4017-989a-2d6e914db3cf" />

- Aggregate UniquePlayer, TheoWin, ActualWin, and CoinIn by Period and NationalityGroup
- Exclude records where Period = 'NA'
<img width="746" height="441" alt="Image" src="https://github.com/user-attachments/assets/811beed4-4077-40c5-9efa-0312b1df41ec" />
  
## Transpose using a Program
- Uses PROC TRANSPOSE to reshape the dataset work.R1 into work.R2.
- Groups data by NationalityGroup using the BY statement.
- Pivots the values of UniquePlayer, CoinIn, ActualWin, and TheoWin across different Period values using the ID statement.
- This transformation converts long-format data into wide-format, making it easier to compare metrics across time periods for each nationality group.
<img width="664" height="181" alt="Image" src="https://github.com/user-attachments/assets/166625ae-5291-455a-a2e1-31b586ad77df" />

## Automated Report Generation
- Configures SAS to send emails via SMTP using the emailhost and emailsys options.
- Uses FILENAME msg EMAIL to define the email recipient, sender, subject, and content type (text/html).
- Embeds a styled HTML message using ODS HTML and escape characters for formatting.
- Generates a detailed report using PROC REPORT:
  - Summarizes gaming performance by Category and NationalityGroup.
  - Compares metrics across periods (Yesterday, P1W, P2W, P3W) and calculates percentage differences.
  - Applies formatting for readability (e.g., bold headers, percent formats).
- Appends a closing message and sends the report as an HTML email.
<img width="772" height="830" alt="Image" src="https://github.com/user-attachments/assets/0a229212-4084-4343-bdba-6479595ac26d" />

## Email Scheduling
- Use the 'Schedule Process Flow' feature in SAS EG to schedule sending of email.
- Set the time and frequency of sending in 'Triggers' tab.
<img width="1163" height="739" alt="Image" src="https://github.com/user-attachments/assets/472f10ba-919a-4b14-867a-2634ce8f1097" />

## Result
- The report was successfully delivered via email at the scheduled time, with the content embedded in HTML format.
<img width="1144" height="785" alt="Image" src="https://github.com/user-attachments/assets/36667dc8-b35b-4ed2-8e4e-9c7af07bc0fa" />

## Technologies Used
- SAS Enterprise Guide
- Base SAS (PROC TRANSPOSE, PROC REPORT, ODS)
- Windows Task Scheduler

