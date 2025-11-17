## 110x data engieneer Assessment Solution (By Tanuj Joshi)

Files added by me:
- sql/schema.sql
- scripts/etl.py

### How to run:

1) Create database tables:
   mysql -u root -p < sql/schema.sql

2) Install python packages:
   pip install pandas mysql-connector-python

3) Run ETL:
   python scripts/etl.py

### Notes:
- ETL loads JSON from data/properties.json into the properties table.
- Simple, clean solution following assessment instructions.

Submitted by:
Tanuj Joshi
Email: joshitanuj1221@gmail.com
