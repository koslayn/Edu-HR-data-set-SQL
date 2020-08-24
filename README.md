# Анализ данных HR отдела
## Источник данных
Набор данных - [Human Resources Data Set](https://www.kaggle.com/rhuebner/human-resources-data-set) разработан Dr. Rich и периодически обновляется.  
Сейчас доступна 13 версия [Codebook - HR Dataset v13](https://rpubs.com/rhuebner/HRCodebook-13) от 9/27/2019  
Также данный набор данных анализировался:  
  * Kathy Sun - в рамках её проекта [Final Project for R](https://rpubs.com/KathySun1/FinalProject)
  * CSV файлы с данными v.9 были получены из [github](https://github.com/patrol7171/HR-Data-Analysis--Dental-Magic/tree/ef3c3dc7169bfec77f35d7fb5e3aced1ef767c58) Patricia Rollins  
  
Данные анализировались в рамках курсового проекат универиситета Skillbox и изначально были представлены БД PostgreSQL на сервере университета.  
  
*Для соблюдение конфиденциальности БД компании Skillbox, при опубликовании данного проекта используется SQLite в которую распакованы таблицы с данными из файлов CSV.*


## Для публичного размещения сделаем следующее:
1. Преобразуем данные из CSV-файлов из репозитория Patricia Rollins в таблицы в БД SQLite (HR.db)
2. В ходе преобразования сделаем следующие корректировки (для соответствия с БД Skillbox):
  * Таблица `salary_grid` - нужно заменить `_` на ` ` (пробел) в названиях столбцов.
  * Таблица `recruiting_costs`:
      * убрать `_2018` в месяцах
      * Добавить пробелы в `EmploymentSource`
      * Создать столбец `Total`
  * Таблица `production_staff`:
      * Заменить `['LastName', 'FirstName']` на `Employee Name`. FirstName + LastName
      * Добавить `id` - просто порядковый номер.
      * `CamelCase` - добавить пробелы `Camel Case`
      * `HireDate` - `Date of Hire`
      * `TermDate` - `TermDate` - не произволить изменений.
      * `AbutmentsPerHourWk1` - `Abutments/Hour Wk1`
      * `AbutmentsPerHourWk2` - `Abutments/Hour Wk2`
      * `Complaints_90Days` - `90-day Complaints`
   * Таблица `hr_dataset`:
       * `id` - Добавить столбец с нумерацией
       * `['LastName', 'FirstName']` - `Employee Name` - FirstName + LastName
       * Перевести в строчные буквы: `['MarriedID', 'MaritalStatusID', 'GenderID', 'EmpStatusID', 'DeptID', 'PerfScoreID', 'Age', 'Zip', 'DOB', 'Sex', 'MaritalDesc', 'CitizenDesc', 'RaceDesc', 'Department', 'Position']`
       * `PerfScoreID` - `perf_scoreid`
       * `EmpstatusID` - `empstatus_id`
       * `Hispanic_Latino` - `Hispanic/Latino`
       * `HireDate` - `Date of Hire`
       * `TerminationDate` - `Date of Termination`
       * `CamelCase` - добавить пробелы `Camel Case`
       * `department`: Изменить `IT - Information Systems` на `IT/IS`
3. Доработаем функцию подключения к базе данных из-за изменения PostgreSQL -> SQLite.
4. Перепроверим SQL-выражения, которые использовались для выполнения запросов.
5. Изменения отметим знаком ⚠