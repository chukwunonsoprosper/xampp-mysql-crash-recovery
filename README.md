# XAMPP MySQL Crash Recovery Guide

This is a simple recovery method I used to fix an XAMPP MySQL crash issue where MySQL would no longer start properly.

> **Disclaimer:** This method worked for me, but it is **not an official XAMPP or MySQL fix**. It is a practical recovery method based on my experience. Your results may vary depending on the cause of the MySQL crash and the state of your database files. **Always make a backup of your existing `data` folder before making any changes.**

## Important

**Make sure XAMPP is completely stopped before doing any of the steps below.**

Do not attempt this while MySQL is running.

---

## 1. Navigate to the XAMPP MySQL directory

Navigate to your XAMPP installation directory on your computer.

The exact location depends on your operating system.

Inside the XAMPP directory, open:

```text
mysql
```

Inside the `mysql` folder, you should find a structure similar to:

```text
mysql/
├── backup/
├── data/
├── bin/
└── ...
```

---

## 2. Create a copy of the `backup` folder

Inside the `mysql` folder, copy the existing:

```text
backup
```

folder.

Paste the copy in the same `mysql` directory.

You may end up with something like:

```text
backup
backup-copy
data
```

The exact name does not matter. You can rename the copied folder to whatever you want.

For example:

```text
backup-copy
```

This gives you a clean backup copy that can be used to recreate the MySQL `data` directory.

---

## 3. Create a copy of the existing `data` folder

Now copy the existing:

```text
data
```

folder.

Paste the copy in the same `mysql` directory.

At this point, you should have something similar to:

```text
mysql/
├── backup/
├── backup-copy/
├── data/
└── data-copy/
```

The copied `data` folder is important because it contains your existing databases and MySQL files.

**Do not delete this copy.**

---

## 4. Delete the original `data` folder

After making sure you have successfully copied the original `data` folder, delete the original:

```text
data
```

folder.

You should now have something similar to:

```text
mysql/
├── backup/
├── backup-copy/
└── data-copy/
```

---

## 5. Rename the backup copy to `data`

Now rename the backup copy you created earlier:

```text
backup-copy
```

to:

```text
data
```

Your directory should now look roughly like:

```text
mysql/
├── backup/
├── data/
└── data-copy/
```

The newly renamed `data` folder is now based on the clean contents of the XAMPP `backup` folder.

---

# Recovering Your Database

At this point, MySQL has a fresh `data` directory, but your project databases are not necessarily there yet.

Your previous database files are still inside:

```text
data-copy
```

## 6. Recover your project database

Open:

```text
data-copy
```

Inside it, you should find the folders representing your project databases.

For example:

```text
data-copy/
├── mysql/
├── performance_schema/
├── phpmyadmin/
├── your_project_database/
└── ...
```

Find the database folder for the project you want to recover.

Copy **only the database folders you need**.

Then paste them into the newly created:

```text
data
```

folder.

For example:

```text
mysql/
├── data/
│   ├── mysql/
│   ├── performance_schema/
│   ├── phpmyadmin/
│   └── your_project_database/
│
└── data-copy/
    └── your_project_database/
```

---

# Recovering the Database Schema, Structure and Content

If you also need to recover the database's schema, structure and saved content, there is another important file you need to restore.

## 7. Locate `ibdata1`

Open your original copied data directory:

```text
data-copy
```

Inside it, look for:

```text
ibdata1
```

This is an important InnoDB data file.

Copy:

```text
ibdata1
```

from:

```text
data-copy
```

and paste it into the newly created:

```text
data
```

folder.

When Windows asks whether you want to replace the existing `ibdata1` file, accept the replacement.

---

## 8. Start XAMPP again

Once you have completed the steps above:

1. Open XAMPP.
2. Start MySQL.
3. Check whether MySQL starts successfully.
4. Open phpMyAdmin.
5. Check your recovered database.
6. Verify that your tables, structure and data are available.

If everything worked correctly, your MySQL server should start without the previous crash and your recovered project database should be accessible again.

---

# Final Directory Structure

After the recovery process, your XAMPP MySQL directory should look roughly like this:

```text
mysql/
├── backup/
├── data/
│   ├── mysql/
│   ├── performance_schema/
│   ├── phpmyadmin/
│   ├── your_project_database/
│   ├── ibdata1
│   └── ...
└── data-copy/
    ├── your_project_database/
    ├── ibdata1
    └── ...
```

The `data-copy` folder is your original data backup, so **do not delete it immediately**. Keep it until you have confirmed that everything has been successfully recovered.

---

## Disclaimer

This procedure is **not an official XAMPP or MySQL recovery procedure**.

It is a recovery method that **worked for me** when I encountered an XAMPP MySQL crash. It may work for similar situations, but it is not guaranteed to work for every MySQL crash or database corruption scenario.

**Always make a backup of your original `data` folder before attempting this procedure.**

If your database contains important or irreplaceable data, consider making additional backups before modifying any MySQL files.

Also, make sure **XAMPP/MySQL is completely stopped before performing these operations.**
