# azure-ad-user
Azure AD User Import Automation using PowerShell &amp; CSV
# Azure AD User Import and Automation

## Project Overview
This project demonstrates how to import users into Azure Active Directory (Azure AD) from a CSV file and automate user creation and role assignment using PowerShell.

### Project Structure
- `import_users.ps1`: PowerShell script to create users in Azure AD.
- `users_template.csv`: Sample CSV template for bulk user import.
- `README.md`: Documentation for the project.

## import_users.ps1
```powershell
# Install AzureAD module if not already installed
# Install-Module -Name AzureAD

# Connect to Azure AD
Connect-AzureAD

# Import CSV file containing user data
$users = Import-Csv -Path "./users_template.csv"

foreach ($user in $users) {
    $passwordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
    $passwordProfile.Password = $user.InitialPassword

    New-AzureADUser -UserPrincipalName $user.UserPrincipalName `
                    -DisplayName $user.DisplayName `
                    -MailNickName $user.DisplayName.Replace(" ", "") `
                    -PasswordProfile $passwordProfile `
                    -AccountEnabled ([System.Convert]::ToBoolean($user.BlockSignIn) -eq $false)
}
```

## users_template.csv
```
UserPrincipalName,DisplayName,InitialPassword,BlockSignIn
exampleuser@domain.onmicrosoft.com,Example User,Password123!,False
anotheruser@domain.onmicrosoft.com,Another User,Password456!,False
```

## README.md
```
# Azure AD User Import and Automation

## Overview
This project demonstrates importing users into Azure Active Directory (Azure AD) using PowerShell and a CSV file. It also covers automating user creation and assigning initial passwords.

## Prerequisites
- Azure AD module for PowerShell
- Azure AD Admin Access
- PowerShell environment

## How to Run
1. Install Azure AD module if not already done:
   ```powershell
   Install-Module -Name AzureAD
   ```
2. Connect to Azure AD:
   ```powershell
   Connect-AzureAD
   ```
3. Update `users_template.csv` with user data.
4. Run the script:
   ```powershell
   ./import_users.ps1
   ```

## Expected Output
- Users will be created in Azure AD.
- Assigned initial passwords.
- Accounts will be enabled based on the `BlockSignIn` column.

## Notes
- Change passwords as per organization policy.
- Use Conditional Access policies to enforce MFA after user creation.
```

## Final Steps
1. Upload these files to your GitHub repository.
2. Add screenshots from Azure AD portal showing users and roles.
3. Provide a link to the repo on your LinkedIn profile or resume.

Good luck with your portfolio!
