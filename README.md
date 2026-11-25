# Confidential Execution with Intel SGX & Gramine

Exam project for *Security of Operating Systems and Cloud* (Parthenope).
Runs an existing C application inside an SGX enclave without rewriting it for the SGX SDK.

## What it does
1. **Isolation**: native vs Gramine execution (virtual PID/UID, confined filesystem, secret injected via manifest)
2. **Attestation**: DCAP quote generation, verification through Azure Attestation (MAA), JWT claims (MRENCLAVE, MRSIGNER, SVN, is-debuggable)
3. **Provisioner**: a Python component that releases the secret only if the MAA signature is valid, MRENCLAVE matches, debug is off and SVN is sufficient
4. **Defense in depth**: OSSEC Syscheck with a custom rule (ID 100002) detecting manifest tampering before enclave launch

## Tested on
Azure confidential VM with real Intel SGX hardware.

## Limitations
The secret is embedded in the manifest for testing, and `sgx.debug` is enabled for the demo.
Production setups should provision it over an encrypted channel and disable debug.

## Stack
C · Gramine · Intel SGX/DCAP · Azure Attestation · OSSEC · Python · Linux
