### Instructions

Open two terminals.

Terminal 1

```
daml install latest # if required
daml build
daml sandbox-classic --ledgerid test-5680-data-migration --sql-backend-jdbcurl "jdbc:postgresql://localhost/sandbox?user=sandbox&password=sandbox" .daml/dist/test-5680-data-migration-0.0.1.dar
```

Terminal 2

```
daml script --dar .daml/dist/test-5680-data-migration-0.0.1.dar --script-name Test:init --ledger-host localhost --ledger-port 6865 --wall-clock-time
daml script --dar .daml/dist/test-5680-data-migration-0.0.1.dar --script-name Test:run --ledger-host localhost --ledger-port 6865 --wall-clock-time
```

Terminal 1

- Terminate the running sandbox process.

- Go to `daml` repo.

```
bazel run //ledger/sandbox:sandbox-binary -- --ledgerid test-5680-data-migration --sql-backend-jdbcurl "jdbc:postgresql://localhost/sandbox?user=sandbox&password=sandbox" "$PRJ_DIR"/stefanobaghino-da/test-5680-data-migration/.daml/dist/test-5680-data-migration-0.0.1.dar
```

Terminal 2

```
daml script --dar .daml/dist/test-5680-data-migration-0.0.1.dar --script-name Test:run --ledger-host localhost --ledger-port 6865 --wall-clock-time
```

If there are no failures, the test is successful and the migration ran successfuly.