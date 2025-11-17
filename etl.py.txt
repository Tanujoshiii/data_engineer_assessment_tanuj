import json
import pandas as pd
import mysql.connector
import os


DATA_FILE = os.path.join(os.path.dirname(os.path.dirname(__file__)), "data", "properties.json")

with open(DATA_FILE, "r", encoding="utf-8") as f:
    data = json.load(f)

df = pd.DataFrame(data)

conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="password",     database="propertydb"
)
cursor = conn.cursor()

insert_sql = """
INSERT INTO properties
(property_id, listing_id, title, description, property_type, status, created_at, updated_at)
VALUES (%s,%s,%s,%s,%s,%s,%s,%s)
"""

for _, row in df.iterrows():
    pid = row.get("id") or row.get("property_id")
    if pid is None:
        continue
    cursor.execute(insert_sql, (
        int(pid),
        row.get("listing_id"),
        row.get("title"),
        row.get("description"),
        row.get("property_type"),
        row.get("status"),
        row.get("created_at"),
        row.get("updated_at")
    ))

conn.commit()
cursor.close()
conn.close()

print("ETL Completed.")
