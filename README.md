# Microsoft Entra ID Governance – User Access Audit

## 📄 Overview
This project demonstrates an **Access Audit** as part of **Microsoft Entra ID Governance**. Using user data exported from **Microsoft Entra ID (formerly Azure AD)**, we analyze the access patterns, identify guest users, and ensure compliance with **identity governance best practices**.

---

## 🧑‍💻 Key Highlights:
- **User Access Export**: CSV file containing user details from **Entra ID**.
- **Audit Analysis**: Identified user types (Members, Guests), object types, and user categories.
- **Governance Actions**: Recommendations for **Access Reviews** and **Lifecycle Management**.

---

## 📊 Sample Data (Extract):
| id                                    | userPrincipalName                             | displayName | objectType | userType | isUser | isGroup | isGuest |
|----------------------------------------|-------------------------------------------------|------------|------------|----------|--------|---------|---------|
| 445d4737-6081-4e91-870e-e7c7e7cd80e0  | thehayesmen_gmail.com#EXT#@thehayesmengmail.onmicrosoft.com | Jerry Minta | user       | Member   | True   | False   | False   |
| 1c94d0ac-3c75-4c9b-b76e-bca9d57bd349  | John@thehayesmengmail.onmicrosoft.com          | Saint John | user       | Member   | True   | False   | False   |

*(Data anonymized for display purposes)*

---

## ⚙️ Audit Insights:
- **Member Users**: Internal users with regular access (e.g., employees).
- **Guest Users**: External users (e.g., vendors, partners) – flagged for review.
- **Group Objects**: Distribution groups and security groups.
- **Orphaned/Inactive Accounts**: Future enhancement to detect disabled or inactive users.

---

## 🛠️ Analysis with Python:
### Sample `analyze_access_audit.py`:
```python
import pandas as pd

# Load CSV data
data = pd.read_csv('entra_id_access_audit.csv')

# Filter Guest Users
guest_users = data[data['userType'] == 'Guest']

# Display Guest Users
print("Guest Users:")
print(guest_users[['displayName', 'userPrincipalName']])

