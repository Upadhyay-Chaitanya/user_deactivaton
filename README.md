# Oracle Cloud User Deactivation Script

This Python script automates deactivation of user accounts in an [Oracle Cloud Infrastructure (OCI) Identity Domain](https://docs.oracle.com/en-us/iaas/Content/Identity/access/domains.htm) (IDCS). Use this utility to selectively deactivate users—either in bulk or by inclusion/exclusion—helping you manage your cloud tenancy securely and efficiently.

---

## Features

- **Lists all users** in the configured OCI Identity Domain
- **Bulk-deactivate** user accounts (disabled in IDCS)
- **Exclusion list**: Always keep specific users active (e.g., admin/service accounts)
- **Optional inclusion list**: Only deactivate users you explicitly want

---

## Prerequisites

- Python 3.x installed
- [OCI Python SDK](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/pythonsdk.htm)  
  ```
  pip install oci
  ```
- A valid [OCI config file](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/sdkconfig.htm) (`~/.oci/config`) with an API key and profile for an admin user
- Access to your Oracle Identity Domain URL
- Domain admin rights to deactivate users

---

## Usage

1. **Set Your OCI config profile and domain_url:**  
   Edit the top of the script to enter your [`profile_name`](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/sdkconfig.htm#ConfigSection) and Identity Domain URL (`domain_url`).

2. **Update lists:**  
   - `users_to_exclude`: Usernames (usually emails) to NEVER deactivate
   - `users_to_include`: (Optional) Usernames to ALWAYS deactivate (leave empty to skip, or use for surgical disabling)

3. **Run the script:**  
   ```sh
   python oci_idcs_user_deactivate.py
   ```

4. **Monitor Output:**  
   The script will print user activity and status to the terminal.

---

## Notes

- **Dry Run** by default for most users except those in `users_to_include`. To bulk-deactivate all (except the excluded list), uncomment the relevant lines in `deactivate_users()`.
- **Be Careful:** Deactivation is immediate and affects user sign-in!
- Make sure to review and test with a small batch before running on production users.
- If you hit API limits or authentication errors, check your config profile and permissions.

---

## Example Configuration

```python
profile_name = "oci01"
domain_url = "https://idcs-xxxxxxxxxxxxxxxxxxxx.identity.oraclecloud.com"

users_to_exclude = [
    "admin1@yourdomain.com",
    "service.account@yourdomain.com"
    # ...etc.
]

users_to_include = [
    # Add usernames to deactivate, or leave empty for full review
]
```

---

## License

MIT License — see [[LICENSE]](https://github.com/Upadhyay-Chaitanya/License/blob/main/MIT) for details.

---

*Created and maintained by Upadhyay-Chaitanya*
