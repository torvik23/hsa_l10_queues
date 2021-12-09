# HSA L10: Queues

## Overview
This is an example project to compare Beanstalkd and Redis (rdb and aof).

## Getting Started

### Preparation
1. Install [Siege](https://github.com/JoeDog/siege) benchmarking tool. If you are using macOS, you can install it via brew
```bash
  brew install siege
```

2. Run the docker containers.
```bash
  docker-compose up -d
```

Be sure to use ```docker-compose down -v``` to clean up after you're done with tests.

## Test scenarios

Compare different scenarios by running next commands:
* For Beanstalkd
```bash
$ siege -c10 -t30S http://localhost:8080/write/beanstalkd
$ siege -c10 -t30S http://localhost:8080/read/beanstalkd
```
* For Redis with AOF persistence mechanism.
```bash
$ siege -c10 -t30S http://localhost:8080/write/redis_aof
$ siege -c10 -t30S http://localhost:8080/read/redis_aof
```
* For Redis with RDB persistence mechanism.
```bash
$ siege -c10 -t30S http://localhost:8080/write/redis_rdb
$ siege -c10 -t30S http://localhost:8080/read/redis_rdb
```

### Write Scenario. Execution time = 30sec.

| Queue/Concurrency | 10 | 25 | 50 | 100 | 1000 |
|---|---|---|---|---|---|
| Beanstalkd | Transactions: 177 hits<br>Data transferred: 0.01 MB<br>Response time: 1.64 secs<br>Transaction rate: 5.92 trans/sec<br>Concurrency: 9.74 | Transactions: 164 hits<br>Data transferred: 0.01 MB<br>Response time: 4.10 secs<br>Transaction rate: 5.56 trans/sec<br>Concurrency: 22.79 | Transactions: 179 hits<br>Data transferred: 0.01 MB<br>Response time: 7.14 secs<br>Transaction rate: 5.98 trans/sec<br>Concurrency: 42.75 | Transactions: 185 hits<br>Data transferred: 0.01 MB<br>Response time: 11.73 secs<br>Transaction rate: 6.23 trans/sec<br>Concurrency: 73.07 | Transactions: 164 hits<br>Data transferred: 0.01 MB<br>Response time: 16.01 secs<br>Transaction rate: 5.53 trans/sec<br>Concurrency: 88.56 |
| Redis with AOF | Transactions: 176 hits<br>Data transferred: 0.01 MB<br>Response time: 1.58 secs<br>Transaction rate: 5.94 trans/sec<br>Concurrency: 9.40 | Transactions: 161 hits<br>Data transferred: 0.01 MB<br>Response time: 4.16 secs<br>Transaction rate: 5.43 trans/sec<br>Concurrency: 22.59 | Transactions: 170 hits<br>Data transferred: 0.01 MB<br>Response time: 6.93 secs<br>Transaction rate: 5.73 trans/sec<br>Concurrency: 39.69 | Transactions: 166 hits<br>Data transferred: 0.01 MB<br>Response time: 12.31 secs<br>Transaction rate: 5.62 trans/sec<br>Concurrency: 69.14 | Transactions: 157 hits<br>Data transferred: 0.01 MB<br>Response time: 15.28 secs<br>Transaction rate: 5.31 trans/sec<br>Concurrency: 81.11 |
| Redis with RDB | Transactions: 178 hits<br>Data transferred: 0.01 MB<br>Response time: 1.65 secs<br>Transaction rate: 5.97 trans/sec<br>Concurrency: 9.83 | Transactions: 166 hits<br>Data transferred: 0.01 MB<br>Response time: 4.09 secs<br>Transaction rate: 5.63 trans/sec<br>Concurrency: 23.02 | Transactions: 164 hits<br>Data transferred: 0.01 MB<br>Response time: 7.49 secs<br>Transaction rate: 5.54 trans/sec<br>Concurrency: 41.50 | Transactions: 159 hits<br>Data transferred: 0.01 MB<br>Response time: 12.76 secs<br>Transaction rate: 5.38 trans/sec<br>Concurrency: 68.69 | Transactions: 152 hits<br>Data transferred: 0.01 MB<br>Response time: 15.72 secs<br>Transaction rate: 4.94 trans/sec<br>Concurrency: 80.46 |

### Read Scenario. Execution time = 30sec.

| Queue/Concurrency | 10 | 25 | 50 | 100 | 1000 |
|---|---|---|---|---|---|
| Beanstalkd | Transactions: 253 hits<br>Data transferred: 0.10 MB<br>Response time: 1.02 secs<br>Transaction rate: 8.67 trans/sec<br>Concurrency: 9.85 | Transactions: 258 hits<br>Data transferred: 0.09 MB<br>Response time: 2.78 secs<br>Transaction rate: 8.64 trans/sec<br>Concurrency: 24.07 | Transactions: 272 hits<br>Data transferred: 0.09 MB<br>Response time: 4.95 secs<br>Transaction rate: 9.30 trans/sec<br>Concurrency: 46.01 | Transactions: 267 hits<br>Data transferred: 0.09 MB<br>Response time: 8.88 secs<br>Transaction rate: 9.08 trans/sec<br>Concurrency: 80.65 | Transactions: 258 hits<br>Data transferred: 0.07 MB<br>Response time: 15.18 secs<br>Transaction rate: 8.65 trans/sec<br>Concurrency: 140.73 |
| Redis with AOF | Transactions: 204 hits<br>Data transferred: 0.07 MB<br>Response time: 1.41 secs<br>Transaction rate: 6.92 trans/sec<br>Concurrency: 9.74 | Transactions: 195 hits<br>Data transferred: 0.07 MB<br>Response time: 3.42 secs<br>Transaction rate: 6.55 trans/sec<br>Concurrency: 22.43 | Transactions: 197 hits<br>Data transferred: 0.07 MB<br>Response time: 6.49 secs<br>Transaction rate: 6.79 trans/sec<br>Concurrency: 44.05 | Transactions: 244 hits<br>Data transferred: 0.08 MB<br>Response time: 9.79 secs<br>Transaction rate: 8.35 trans/sec<br>Concurrency: 81.73 | Transactions: 233 hits<br>Data transferred: 0.08 MB<br>Response time: 15.32 secs<br>Transaction rate: 7.87 trans/sec<br>Concurrency: 120.60 |
| Redis with RDB | Transactions: 215 hits<br>Data transferred: 0.07 MB<br>Response time: 1.36 secs<br>Transaction rate: 7.20 trans/sec<br>Concurrency: 9.77 | Transactions: 204 hits<br>Data transferred: 0.07 MB<br>Response time: 3.40 secs<br>Transaction rate: 6.92 trans/sec<br>Concurrency: 23.50 | Transactions: 219 hits<br>Data transferred: 0.07 MB<br>Response time: 5.98 secs<br>Transaction rate: 7.40 trans/sec<br>Concurrency: 44.29 | Transactions: 215 hits<br>Data transferred: 0.07 MB<br>Response time: 10.64 secs<br>Transaction rate: 7.32 trans/sec<br>Concurrency: 77.88 | Transactions: 212 hits<br>Data transferred: 0.07 MB<br>Response time: 14.92 secs<br>Transaction rate: 7.16 trans/sec<br>Concurrency: 106.83 |
