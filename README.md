# Reference: https://docs.djangoproject.com/en/5.1/howto/initial-data/

# dumpdata command
- It is a django management command, which can be use to backup(export) you model instances or whole database

# dumpdata for basic database 
- python manage.py dumpdata > db.json

# dumpdata for backup specific app
- python manage.py dumpdata auth > admin.json

# dumpdata for backup specific table
- python manage.py dumpdata auth.permission > permission.json

# dumpdata (--exclude)
You can use --exclude option to specify apps/tables which don't need being dumped
Following command will dump the whole database with out including auth.permission table content
- python manage.py dumpdata --exclude auth.permission > db.json

# dumpdata (--indent)
By default, dumpdata will output all data on a single line. It isn’t easy for humans to read
You can use the --indent option to pretty-print the output with a number of indentation spaces
- python manage.py dumpdata auth.user --indent 2 > user.json

# dumpdata (--format)
- python manage.py dumpdata auth.user --indent 2 --format xml > user.xml

# loaddata command - This command can be use to load the fixtures(database dumps) into database
Problems: UnicodeDecodeError: 'utf-8' codec can't decode byte 0xff in position 0: invalid start byte
Solutions:
- Open the file in regular notepad
- Select save as
- Select encoding "UTF-8"
- Save the file.
# Executing command:
- python manage.py loaddata user.json

# Restore fresh database
When you backup whole database by using dumpdata command, it will backup all the database tables
If you use this database dump to load the fresh database(in another django project), it can be causes IntegrityError (If you loaddata in same database it works fine)
To fix this problem, make sure to backup the database by excluding contenttypes and auth.permissions tables

- python manage.py dumpdata --indent 2  --exclude auth.permission --exclude contenttypes > db.json








