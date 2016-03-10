# List table index names and sizes.

While from the PSQL shell `\d <TABLENAME>` is enough, from the python shell is:

    >>> import psycopg2
    >>> conn = psycopg2.connect(user='USERNAME', password='PASSWORD',
    ...                         database='DATABASE', host='HOST')
    >>> cur = conn.cursor()
    >>> sql = \
    ... ''' SELECT
    ...       i.relname,
    ...       i.relpages
    ...     FROM
    ...        pg_class t,
    ...        pg_class i,
    ...        pg_index ix
    ...     WHERE
    ...        t.relname = %s
    ...        and t.oid = ix.indrelid
    ...        and i.oid = ix.indexrelid; '''
    >>> cur.execute(sql, [<TABLENAME>])
    >>> indexes = cur.fetchall()
    >>> for index in indexes: print '%s (%.1fGb)' % (index[0], index[1]*8.0/2**20)

Each page is typically 8Kb. `relpages` is only updated when the database is
vacuumed or analyzed.








