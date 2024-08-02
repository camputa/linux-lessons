# Backup Documentation: WordPress Website

**Objective:** Documenting backup procedures for a WordPress website hosted on Ubuntu Linux to ensure data integrity and facilitate recovery in case of data loss or system failure.

## 1. Backup Schedule

**Backup Type:** Incremental Backup  
**Frequency:** Daily  
**Backup Time:** 02:00 AM  
**Retention Policy:** Keep daily backups for 7 days  
**Backup Location:** `/backup/wordpress`  
**Automation:** Scheduled using cron jobs

## 2. Backup Procedures

### Files Backup

**Web Directory:** /var/www/website

1. **Procedure:**
   - Create a compressed archive (`tar.gz`) of the web directory.
   - Example Command:

     ```bash
     tar -czf /backup/wordpress/website_backup_$(date +%Y%m%d).tar.gz -C /var/www/website/ .
     ```

   - This command compresses the `/var/www/website` directory into a dated archive file in the `/backup/wordpress` directory.

2. **Automation:**
   - Add a cron job to automate daily backups:

     ```bash
     0 2 * * * tar -czf /backup/wordpress/website_backup_$(date +\%Y\%m\%d).tar.gz -C /var/www/website/ .
     ```

   - Adjust the timing (`0 2 * * *`) as per your preference.

### Database Backup

**MySQL Database:** wp_production_website

1. **Procedure:**
   - Export the MySQL database to a SQL file.
   - Example Command:

     ```bash
     mysqldump -u username -p wp_production_website > /backup/wordpress/wp_production_website_backup_$(date +%Y%m%d).sql
     ```

   - Replace `username` with your MySQL username.

2. **Automation:**
   - Schedule automatic database backups using cron:

     ```bash
     0 3 * * * mysqldump -u username -p wp_production_website > /backup/wordpress/wp_production_website_backup_$(date +\%Y%m%d).sql
     ```

   - Adjust the timing (`0 3 * * *`) to suit your needs.

## 3. Restoration Procedures

### Files Restoration

1. **Procedure:**
   - Extract the web directory backup using `tar`.
   - Example Command:

     ```bash
     tar -xzf /backup/wordpress/website_backup_YYYYMMDD.tar.gz -C /var/www/
     ```

   - Replace `YYYYMMDD` with the date of the backup file.

### Database Restoration

1. **Procedure:**
   - Restore the MySQL database backup using `mysql`.
   - Example Command:

     ```bash
     mysql -u username -p wp_production_website < /backup/wordpress/wp_production_website_backup_YYYYMMDD.sql
     ```

   - Replace `YYYYMMDD` with the date of the backup file.

## 4. Verification Procedures

### Verify Backup Integrity

- **File Backup:**
  - Check the integrity of the compressed archive (`tar.gz`) by verifying its size and checksum.
  - Example Command:

       ```bash
       md5sum /backup/wordpress/website_backup_YYYYMMDD.tar.gz
       ```

  - Compare the checksum with the original to ensure the file hasn't changed.

- **Database Backup:**
  - Verify the integrity of the MySQL dump file by examining its size and contents.
  - Example Command:

       ```bash
       wc -l /backup/wordpress/wp_production_website_backup_YYYYMMDD.sql
       ```

  - Count the number of lines to ensure it matches the expected database structure and data.

### Test Restoration

- Periodically restore backups to a test environment.
- Validate that the website and database can be fully restored without errors.
- Document any issues encountered and update procedures accordingly.

## 5. Notes

- **Security:** Implement secure storage practices for backup files, including encryption and access controls.
- **Documentation Updates:** Maintain up-to-date documentation to reflect changes in backup procedures and configurations.
