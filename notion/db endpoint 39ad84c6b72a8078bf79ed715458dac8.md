# db endpoint

```json
proxy-rds.proxy-cnqskux1bi2d.ap-northeast-1.rds.amazonaws.com
```

```json
START RequestId: 2148cafa-a196-4e81-9062-2c04ccf78a43 Version: $LATEST
{"level":"INFO","location":"lambda_handler:24","message":"Connect to proxy-rds.proxy-cnqskux1bi2d.ap-northeast-1.rds.amazonaws.com","timestamp":"2026-07-11 23:43:44,869+0000","service":"db_client","cold_start":true,"function_name":"DBClient","function_memory_size":"128","function_arn":"arn:aws:lambda:ap-northeast-1:761718984289:function:DBClient","function_request_id":"2148cafa-a196-4e81-9062-2c04ccf78a43","xray_trace_id":"1-6a52d530-0ba60ad2785ec2ae7971737c"}
[ERROR] OperationalError: (1045, "Access denied for user 'pxyuh'@'10.0.1.102' (using password: YES)")
Traceback (most recent call last):
  File "/opt/python/aws_lambda_powertools/logging/logger.py", line 447, in decorate
    return lambda_handler(event, context, *args, **kwargs)
  File "/var/task/app.py", line 25, in lambda_handler
    connection = pymysql.connect(
  File "/var/task/pymysql/connections.py", line 358, in __init__
    self.connect()
  File "/var/task/pymysql/connections.py", line 664, in connect
    self._request_authentication()
  File "/var/task/pymysql/connections.py", line 968, in _request_authentication
    auth_packet = self._process_auth(plugin_name, auth_packet)
  File "/var/task/pymysql/connections.py", line 1001, in _process_auth
    return _auth.caching_sha2_password_auth(self, auth_packet)
  File "/var/task/pymysql/_auth.py", line 221, in caching_sha2_password_auth
    pkt = _roundtrip(conn, scrambled)
  File "/var/task/pymysql/_auth.py", line 120, in _roundtrip
    pkt = conn._read_packet()
  File "/var/task/pymysql/connections.py", line 772, in _read_packet
    packet.raise_for_error()
  File "/var/task/pymysql/protocol.py", line 221, in raise_for_error
    err.raise_mysql_exception(self._data)
  File "/var/task/pymysql/err.py", line 143, in raise_mysql_exception
    raise errorclass(errno, errval)
END RequestId: 2148cafa-a196-4e81-9062-2c04ccf78a43
REPORT RequestId: 2148cafa-a196-4e81-9062-2c04ccf78a43	Duration: 308.12 ms	Billed Duration: 880 ms	Memory Size: 128 MB	Max Memory Used: 92 MB	Init Duration: 571.09 ms	

```

```json
import os

import boto3
import pymysql
from aws_lambda_powertools import Logger
from aws_lambda_powertools.utilities import parameters

REGION = os.environ["AWS_REGION"]
DB_ENDPOINT = os.environ["DB_ENDPOINT"]
DB_PORT = os.environ["DB_PORT"]
DB_USERNAME = os.environ["DB_USERNAME"]
DB_NAME = os.environ["DB_NAME"]
TABLE_NAME = os.environ["TABLE_NAME"]

logger = Logger()
rds = boto3.client("rds")

@logger.inject_lambda_context
def lambda_handler(event, context):
    token = rds.generate_db_auth_token(
        DBHostname=DB_ENDPOINT, Port=DB_PORT, DBUsername=DB_USERNAME, Region=REGION
    )

    logger.info(f"Connect to {DB_ENDPOINT}")
    connection = pymysql.connect(
        host=DB_ENDPOINT,
        port=int(DB_PORT),
        user=DB_USERNAME,
        password=token,
        database=DB_NAME,
        cursorclass=pymysql.cursors.DictCursor,
        ssl={"ca": "AmazonRootCA1.pem"},
        autocommit=True,
    )

    with connection:
        logger.info(f"Success Connect to Database")
        with connection.cursor() as cursor:
            sql = f"SELECT answer FROM {TABLE_NAME};"
            cursor.execute(sql)
            query_results = cursor.fetchall()

    return query_results
```