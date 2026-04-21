## Mina Mesa PreFlight Setup Error

I hv tried the two approaches below to setup Mina Daemon, but got the **same** error(as the page bottom), which should be related to env parameters and I ever met loong ago. 

**This error has been also met by a discord user: [here](https://discord.com/channels/484437221055922177/1450202839430201506/1450318356493111306).**

TODO: Need find out the root cause.


### Option1: steps as per https://docs.minaprotocol.com/network-upgrades/mesa/preflight-network

simply execute the script as per docs:
```
docker run --name mina-mesa-preflight -d \
  -p 8302:8302 \
  --restart=always \
  gcr.io/o1labs-192920/mina-daemon:4.0.0-preflight1-b649c79-bookworm-mesa \
  daemon \
  --peer-list-url https://storage.googleapis.com/o1labs-gitops-infrastructure/mina-mesa-network/mina-mesa-network-seeds.txt
```

but got the **same** error as the page bottom.


### Option1: steps as per discord suggestion
With reference to [discord user's case](https://discord.com/channels/484437221055922177/1450202839430201506/1457622372830937184) and also [this sample](https://discord.com/channels/484437221055922177/1450202839430201506/1469471117944160380), kindly save the script into local [docker-compose.yaml](./docker-compose.yaml)

then, execute the script below:
```
docker compose up -d && docker compose logs -f
```

but got the errors as below:
```
generate_wallet_key-1  | Using password from environment variable MINA_PRIVKEY_PASS
generate_wallet_key-1  | Keypair generated
generate_wallet_key-1  | Public key: B62qqGZSdytjor6LXdJXMvwBRrDC2v4bTRJyQiB42YnCc6t4LvSNkQd
generate_wallet_key-1  | Raw public key: CB52E6A8DC1E763FA15731428A3B76168D6597D9EC7210F65B9D03A3B6BD7A3E
mina_block_producer-1  | 2026-04-21 17:06:05 UTC [Info] Mina daemon is booting up; built with commit "b649c795104d4b6149a0b69c5e5b93ff6e3e2138"
mina_block_producer-1  |
mina_block_producer-1  | 2026-04-21 17:06:05 UTC [Info] Booting may take several seconds, please wait
mina_block_producer-1  |
mina_block_producer-1  | 2026-04-21 17:06:05 UTC [Info] Reading configuration files $config_files
mina_block_producer-1  |   config_files: [ "/var/lib/coda/config_b649c795.json", "/root/.mina-config/daemon.json" ]
mina_block_producer-1  | 2026-04-21 17:06:05 UTC [Warn] Could not read configuration from "/root/.mina-config/daemon.json"
mina_block_producer-1  |
mina_block_producer-1  | 2026-04-21 17:06:05 UTC [Info] Initializing with runtime configuration. Ledger name: null
mina_block_producer-1  |
mina_block_producer-1  | 2026-04-21 17:06:05 UTC [Info] Using the compiled constraint constants
mina_block_producer-1  |
mina_block_producer-1  | 2026-04-21 17:06:29 UTC [Error] Could not find or generate a "genesis_ledger" for $root_hash
mina_block_producer-1  |   root_hash: "jwQkrmEhsdde6T3gR98A7GPZSqsfRGP1G2Hi7PJuKLfh3s64Sa3"
mina_block_producer-1  | 2026-04-21 17:06:29 UTC [Info] Initializing with runtime configuration. Ledger source: $name
mina_block_producer-1  |   name: "jwQkrmEhsdde6T3gR98A7GPZSqsfRGP1G2Hi7PJuKLfh3s64Sa3"
mina_block_producer-1  | 2026-04-21 17:06:29 UTC [Error] Could not send error report: Node_error_service was not configured
mina_block_producer-1  |
mina_block_producer-1  | 2026-04-21 17:06:29 UTC [Fatal] Unhandled top-level exception: $exn
mina_block_producer-1  | Generating crash report
mina_block_producer-1  |   exn: {
mina_block_producer-1  |   "sexp": [
mina_block_producer-1  |     "monitor.ml.Error",
mina_block_producer-1  |     "Could not find a ledger tar file for hash 'jwQkrmEhsdde6T3gR98A7GPZSqsfRGP1G2Hi7PJuKLfh3s64Sa3'",
mina_block_producer-1  |     [
mina_block_producer-1  |       "Raised at Base__Error.raise in file \"src/error.ml\" (inlined), line 8, characters 14-30",
mina_block_producer-1  |       "Called from Mina_cli_entrypoint.load_config_files.(fun) in file \"src/app/cli/src/cli_entrypoint/mina_cli_entrypoint.ml\", line 144, characters 8-23",
mina_block_producer-1  |       "Called from Async_kernel__Deferred1.M.map.(fun) in file \"src/deferred1.ml\", line 17, characters 40-45",
mina_block_producer-1  |       "Called from Async_kernel__Job_queue.run_job in file \"src/job_queue.ml\" (inlined), line 128, characters 2-5",
mina_block_producer-1  |       "Called from Async_kernel__Job_queue.run_jobs in file \"src/job_queue.ml\", line 169, characters 6-47",
mina_block_producer-1  |       "Caught by monitor coda"
mina_block_producer-1  |     ]
mina_block_producer-1  |   ],
mina_block_producer-1  |   "backtrace": [
mina_block_producer-1  |     "Raised at Base__Error.raise in file \"src/error.ml\" (inlined), line 8, characters 14-30",
mina_block_producer-1  |     "Called from Mina_cli_entrypoint.load_config_files.(fun) in file \"src/app/cli/src/cli_entrypoint/mina_cli_entrypoint.ml\", line 144, characters 8-23",
mina_block_producer-1  |     "Called from Async_kernel__Deferred1.M.map.(fun) in file \"src/deferred1.ml\", line 17, characters 40-45",
mina_block_producer-1  |     "Called from Async_kernel__Job_queue.run_job in file \"src/job_queue.ml\" (inlined), line 128, characters 2-5",
mina_block_producer-1  |     "Called from Async_kernel__Job_queue.run_jobs in file \"src/job_queue.ml\", line 169, characters 6-47"
mina_block_producer-1  |   ]
mina_block_producer-1  | }
mina_block_producer-1  | 2026-04-21 17:06:29 UTC [Warn] Shutdown before Mina instance was created, not saving a visualization
mina_block_producer-1  |
mina_block_producer-1  |
mina_block_producer-1  |
mina_block_producer-1  |   ☠  Mina Daemon crashed.
mina_block_producer-1  |    The Mina Protocol developers would like to know why!
mina_block_producer-1  |
mina_block_producer-1  |     Please:
mina_block_producer-1  |       Open an issue:
mina_block_producer-1  |         <https://github.com/MinaProtocol/mina/issues/new>
mina_block_producer-1  |
mina_block_producer-1  |       Briefly describe what you were doing and attach the crash report /root/.mina-config/coda_crash_report_2026-04-21_17-06-29.718911.tar.gz
mina_block_producer-1  |
mina_block_producer-1  |
mina_block_producer-1 exited with code 1 (restarting)
```



