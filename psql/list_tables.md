# List all table names of a database.

While from the PSQL shell `\dt` is enough, from the python shell is:

    >>> import psycopg2
    >>> conn = psycopg2.connect(user='USERNAME', password='PASSWORD',
    ...                         database='DATABASE', host='HOST')
    >>> cur = conn.cursor()
    >>> sql = ('SELECT table_name FROM information_schema.tables WHERE '
    ...        'table_schema=%s AND table_type=%s ORDER BY table_name;')
    >>> cur.execute(sql, ['public', 'BASE TABLE'])
    >>> print [i[0] for i in cur.fetchall()]
    ['table1', 'table2', 'table3']

The second condition, `table_type=BASE TABLE`, can be avoided if you don't mind
Postgres returning views as well.






