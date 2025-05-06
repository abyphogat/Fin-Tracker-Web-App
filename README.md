
# **FINTRACK**

<br/>

# **Project Summary:**
- A progressive web application
- Assist users in managing their personal finances
- Allows users to customize their expense categories
- Also Tracks users’ multiple bank accounts on different expense categories and visualize them in charts.
- The account transactions(income/expenses) are fetched from a Mock API working as a Bank.

<br/>
<br/>

# **Tech Stack:**
### **Backend**
- Java 17
- SpringBoot Framework

### **Frontend**
- Node 18.15.0
- ReactJS

### **Database**
- MySQL

<br/>
<br/>

# **Implemented set of features:**

| Features                                                    | Status   |
|-------------------------------------------------------------|----------|
| User Authentication                                         | ACHIEVED |
| Feature to add User Accounts, Incomes, Expenses, Categories | ACHIEVED |
| Visualizing Expenses                                        | ACHIEVED |
| Mock Bank API (Implemented after Mid-Term)                  | ACHIEVED |
| Integration Tests                                           | ACHIEVED |
| CI/CD Pipeline                                              | ACHIEVED |

<br/>
<br/>

# **DEPENDENCIES**
## **Frontend**

The following dependencies are required to run this project:

| Dependency                   | Version   |
|------------------------------|-----------|
| @emotion/react               | ^11.10.6 |
| @emotion/styled              | ^11.10.6 |
| @mui/icons-material          | ^5.11.9   |
| @mui/material                | ^5.11.10  |
| @mui/system                  | ^5.11.12 |
| @testing-library/jest-dom    | ^5.16.5  |
| @testing-library/react       | ^13.4.0   |
| @testing-library/user-event | ^14.4.3  |
| axios                        | ^1.3.3    |
| bcryptjs                     | ^2.4.3    |
| bootstrap                    | ^5.2.3    |
| buffer                       | ^6.0.3    |
| chart.js                     | ^4.2.1    |
| chartjs-plugin-datalabels    | ^2.2.0    |
| classnames                   | ^2.3.2    |
| crypto                       | npm:crypto-browserify |
| crypto-browserify            | 3.12.0   |
| js-cookie                    | ^3.0.1    |
| lodash                       | ^4.17.21 |
| react                        | ^18.2.0  |
| react-bootstrap              | ^2.7.1    |
| react-chartjs-2              | ^5.2.0    |
| react-dom                    | ^18.2.0  |
| react-redux                  | ^8.0.5   |
| react-router                 | ^6.8.1   |
| react-router-dom             | ^6.8.1   |
| react-scripts                | 5.0.1    |
| redux                        | ^4.2.1   |
| redux-logger                 | ^3.0.6   |
| redux-persist                | ^6.0.0   |
| redux-thunk                  | ^2.4.2   |
| stream                       | npm:stream-browserify |
| web-vitals                   | ^3.1.1   |


## **Backend**

Include all these dependencies in your pom.xml file

| Dependency                   | Version       |
| ---------------------------- | ------------- |
| spring-boot-starter-web      |               |
| spring-boot-starter-web-services |             |
| spring-boot-starter-data-jpa | 3.0.2         |
| spring-boot-devtools         |               |
| spring-boot-configuration-processor |       |
| spring-boot-starter-test     |               |
| spring-boot-starter-security |               |
| spring-boot-starter-oauth2-resource-server | 3.0.2 |
| spring-boot-starter-validation |             |
| jaxb-api                      | 2.2.7        |
| jaxb-impl                     | 2.2.5-b10    |
| jjwt                          | 0.9.1        |
| hibernate-core                | 6.1.6.Final  |
| hibernate-entitymanager       | 5.6.15.Final |
| hibernate-validator           | 5.4.1.Final  |
| mysql-connector-java          | 5.1.26       |
| validation-api                | 2.0.1.Final  |
| jakarta.persistence-api       | 3.1.0        |
| spring-boot-starter-jdbc      | 3.0.2        |
| lombok                        |               |
| junit                         | 4.12         |
| spring-security-test          | 6.0.2        |

<br/>
<br/>

# **BUILD INSTRUCTIONS**
1. First run the backend using following steps from the project root folder:

    ```
    > cd backend
    # generate jar file for the backend
    > mvn clean package spring-boot:repackage -DskipTests=true
    # run the jar file
    > java -jar ./target/backend-0.0.1-SNAPSHOT.jar -Dspring.datasource.url=<database_url> -Dspring.datasource.username=<database_username> -Dspring.datasource.password=<database_password>
    ```
    Backend service will start running on http://localhost:8080

    Note: database url looks like: jdbc:mysql://<domain_name>:3306/<database_name>

2. Run the frontend service using following steps from the project root folder:

    1. create .env file same as [.env.sample](./frontend/.env.sample) under [frontend](/frontend/) and provide base url of the backend service
        Note: For localhost the base url will be http://localhost:8000 
    2. run the following code:
        
        ```
        > cd ./frontend
        > npm install
        > npm start
        ```
    
    Note: The frontend service will start running on http://localhost:3000

<br/>
<br/>

# **DEPLOYMENT INSTRUCTIONS**

`build-backend` and `build-frontend` jobs in [.gitlab-ci.yml](.gitlab-ci.yml) generates all the artifacts needed to deploy the backend and frontend

* Download the artifacts of `build-backend` job
* The `.jar` to run the backend service is saved under `backend/target/backend-0.0.1-SNAPSHOT.jar` path in the artifact
* Upload the `.jar` file on the server and run, 

    ```
    > java -jar ./target/backend-0.0.1-SNAPSHOT.jar -Dspring.datasource.url=<database_url> -Dspring.datasource.username=<database_username> -Dspring.datasource.password=<database_password>
    ```

* Download the artifacts of `build-frontend` job
* The `build` files to run the frontend service is saved at `frontend` path in the artifact
* Upload entire `build` folder to the server and run,

    ```
    > serve -s build
    ```

**Note**: The build artifact for the frontend service is only configured to call the backend service running at http://172.17.1.244:8080 (network address of the deployment server). If the backend service is running at different ip then change `BACKEND_API_URL`
variable in the Gitlab CI/CD configurations. The resolution of the limitation is to assign domain name to the backend service and provide that as the value of `BACKEND_API_URL` environment variable in GitLab CI/CD configuration.


<br/>
<br/>

# **GitLab Jobs**
* `build-frontend`: Builds deployment artifacts for the frontend service
* `build-backend`: Builds deployment artifacts for the backend service
* `test`: Run all the unit tests and integration test in the backend and generates **Jacoco** report
* `smell-check`: Run the Designite tools and generates artifacts of smell reports

<br/>
<br/>

# **USAGE SCENARIO**
Following are the usage scenarios covering all the features implemented in this project:

<br/>

## **Authentication Workflow**
User will be landed on the **Login** page when they visit the FINTRACK website.

![Landing page](/Resources/Screenshots/login.png)


<br/>

To signup, the user can click on the **Sign up** button that is on the top-right corner of the screen. The Signup button will redirect the user to the **Sign Up** page.

![Signup](/Resources/Screenshots/signup.png)


The user can fill out the details of the signup form to signup for the website.

![Signup form filled](/Resources/Screenshots/correct_password_signup.png)

There are also validations added for Password and Confirm password and until password and confirm password do not match, the signup button will be inactive.

![Signup password not matching](/Resources/Screenshots/incorrect_password_signup.png)

After, the signup is successful, the user will be redirected to the **Login** page to login into the website after signup.

![Login popup](/Resources/Screenshots/login_with_creds.png)

After successful Login process, the user will be redirected to the **Dashboard** page.

<br/>

## **Dashboard Module**
The user will be landed to the Dashboard page where all the charts - Account balance, Income, Expense and Category, are displayed for the user to help visualize all the transactions that have occurred.

![Dashboard](/Resources/Screenshots/dashboard_all.png)
![Dashboard chart](/Resources/Screenshots/chart_example.png)

The user is provided with 2 options for chart display - all, last 15 days on the bottom of the page.
![Dashboard](/Resources/Screenshots/dashboard_all.png)
![Dashboard](/Resources/Screenshots/dashboard_last_15.png)

<br/>

## **SideBar Menu**
On the top-left corner there is a Menu option which opens a **Sidebar Menu** for the user to navigate through the website.

![Sidebar menu](/Resources/Screenshots/sidebar_menu.png)

<br/>

## **Account Module**
When the user selects the **Account** option from the Sidebar menu, the user is redirected to the Account page. If the user is a new user, and hasn't added any accounts yet, then the account list will be empty.

![Account page](/Resources/Screenshots/account_before.png)

The user can add a Account by clicking on the *Add Account* button that is located at the top-right corner and a pop will be opened asking for the account details.

![Account popup](/Resources/Screenshots/add_account_with_data.png)
![add account validation](/Resources/Screenshots/add_account_validation.png)


On clicking the **Add** button on the Add account popup, the account details will be saved in the Database and a toaster notification saying the same will be displayed for the user and will be reflected in the account list as well.

![account added successfully notification](/Resources/Screenshots/account_added_successfully.png)

If the user wants to edit Account details they can edit it by clicking on the *edit* button.

![edit account popup](/Resources/Screenshots/edit_account_popup.png)

After making the necessary changes, the user can click on the *Save* button to update the account details which will be reflected in the list and user will receive a notification.

![edit account successfully](/Resources/Screenshots/edit_account_successful.png)

<br/>

## **Transaction Module**

When the user selects the Transaction option from the sidebar menu, they are redirected to the Transaction page.

The Transaction page essentially lists two types of transactions - Expense and Income. By default, the Expense tab is selected to list out all the expenses. This transactions are gathered using two approaches - Bank transactions and user's manually added transactions.

![transaction page](/Resources/Screenshots/transactions_list_all.png)

At the top-left corner there is a dropdown, that has all the accounts that the user has added. 

![account dropdown](/Resources/Screenshots/transactions_account_drpdwn.png)

By selecting a particular account, the expenses occurred from that account will be listed out.

![transaction for particular account](/Resources/Screenshots/transactions_list_selected_account_expense.png)
![transaction for particular account](/Resources/Screenshots/transactions_list_selected_account_income.png)

The user can add, update, delete any transactions they want.

**ADD TRANSACTION**

To add a new transaction, the user can click on the *Add Transaction* button located at the top-right corner and a popup will open up.

![new transaction popup](/Resources/Screenshots/add_transaction_expense_before.png)

**EXPENSE**

![new transaction popup](/Resources/Screenshots/add_transaction_expense_select_account_drpdwn.png)

The user can also select a category for the transaction and also add a new category while adding a transaction.

![category dropdown](/Resources/Screenshots/add_transaction_expense_category_drpdwn.png)
![add category popup](/Resources/Screenshots/add_category.png)

<br/>

![add transaction calender](/Resources/Screenshots/add_transaction_expense_calender.png)

On clicking the **Add** button, the transaction will be saved, reflected in the list and a notification will be received by the user.

![transaction added successfully](/Resources/Screenshots/add_transaction_expense_successfull.png)

<br/>

**INCOME**

![add income popup](/Resources/Screenshots/add_transaction_income_popup.png)

![add income filled data](/Resources/Screenshots/add_transction_income.png)

![add income validation](/Resources/Screenshots/add_transaction_income_validation.png)

<br/>

**EDIT TRANSACTION**

When the user wants to edit a transaction, they can edit it by clicking the edit button and make the required changes and click on *Save* button. On a successful save, a notification will be received by the user.

![edit transaction expense](/Resources/Screenshots/edit_transaction_expense_popup.png)
![edit transaction expense](/Resources/Screenshots/edit_transaction_income_popup.png)

<br/>

![edit transaction expense success](/Resources/Screenshots/edit_transaction_expense_successfull.png)
![edit transaction income success](/Resources/Screenshots/edit_transaction_income_success.png)

<br/>

**DELETE TRANSACTION**

When the user wants to delete a transaction, they can delete it by clicking the delete button. On a successful delete, a notification will be received by the user.

![delete expense success](/Resources/Screenshots/delete_expense.png)
![delete income success](/Resources/Screenshots/delete_income.png)

<br/>
<br/>

**Deployed at**: http://172.17.1.244:3000/ (require dal network/vpn)
