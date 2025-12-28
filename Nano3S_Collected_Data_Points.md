# Nano 3S - All Collected Data Points

This document lists all data points currently being collected and parsed from the Avalon Nano 3S.

## Data Sources

The Nano 3S data is collected from 4 API commands:
1. **summary** - Basic statistics and hashrate
2. **estats** - Extended statistics (temperature, fan, power details)
3. **version** - Firmware and hardware version information
4. **pools** - Pool connection and statistics

---

## 1. Summary Command Data (`summary`)

### Status & Timing
- **Status** (`status`) - Response status code (S = Success)
- **When** (`when`) - Timestamp of the response
- **Code** (`code`) - Status code number
- **Msg** (`msg`) - Status message
- **Description** (`description`) - Response description
- **Elapsed** (`elapsed`) - Total elapsed time since miner started (seconds)

### Hashrate Metrics
- **MHS av / AverageHash** (`mhs_av`, `average_hash`) - Average hashrate in MH/s (converted to TH/s)
- **MHS 5s / RealtimeHash** (`mhs_5s`, `realtime_hash`) - Current hashrate over last 5 seconds (converted to TH/s)
- **MHS 1M** (`mhs_1m`) - 1 minute average hashrate (parsed but not stored)
- **MHS 5M** (`mhs_5m`) - 5 minute average hashrate (parsed but not stored)
- **MHS 15M** (`mhs_15m`) - 15 minute average hashrate (parsed but not stored)

### Share Statistics
- **Accepted** (`accepted`) - Total accepted shares
- **Rejected / Reject** (`reject`) - Total rejected shares
- **Rejected Percentage** (`rejected_percentage`) - Calculated: (Rejected / (Accepted + Rejected)) * 100
- **Found Blocks** (`found_blocks`) - Number of blocks found
- **Discarded** (`discarded`) - Number of discarded shares
- **Stale** (`stale`) - Number of stale shares
- **Diff1 Shares** (`diff1_shares`) - Difficulty 1 shares

### Work & Network Metrics
- **Getworks** (`getworks`) - Total getwork requests
- **Get Failures** (`get_failures`) - Number of failed getwork requests
- **Local Work** (`local_work`) - Local work units
- **Remote Failures** (`remote_failures`) - Number of remote connection failures
- **Network Blocks** (`network_blocks`) - Current network block count
- **Total MH** (`total_mh`) - Total megahashes processed
- **Diff1 Work** (`diff1_work`) - Difficulty 1 work units
- **Total Hashes** (`total_hashes`) - Total hashes processed
- **Last Valid Work** (`last_valid_work`) - Timestamp of last valid work

### Difficulty Metrics
- **Difficulty Accepted** (`difficulty_accepted`) - Total difficulty of accepted shares
- **Difficulty Rejected** (`difficulty_rejected`) - Total difficulty of rejected shares
- **Difficulty Stale** (`difficulty_stale`) - Total difficulty of stale shares
- **Last Share Difficulty** (`last_share_difficulty`) - Difficulty of the last share submitted
- **Best Share** (`best_share`) - Best share difficulty found (from summary, not pool-specific)

### Power
- **Power** (`power`) - Power consumption in watts

### Fields Parsed But Not Stored
- Hardware Errors
- Utility
- Work Utility
- Device Hardware%
- Device Rejected%
- Pool Rejected%
- Pool Stale%
- Last getwork

---

## 2. Extended Statistics Command Data (`estats`)

### Temperature Metrics
- **OTemp / Operating Temperature** (`otemp`) - Current operating temperature (°C)
- **TMax / Max Temperature** (`tmax`) - Maximum temperature reached (°C)
- **TAvg / Average Temperature** (`tavg`) - Average temperature (°C)

### Fan Metrics
- **Fan1 / Fan Status** (`fan1`, `fan_status`) - Fan 1 speed (RPM)
- **FanR** (`fanr`) - Fan speed percentage (%)

### Hashrate (from estats)
- **GHSspd** (`ghsspd`) - Current hashrate in GH/s

### Power & Performance
- **PS** (`ps`) - Power status array (raw string)
- **Power** (`power`) - Power in watts (extracted from PS array if not set from summary)

### System Information
- **Ver / MM Version** (`ver`, `mm_ver`) - Firmware version string from MM section
- **Working Mode** (`workingmode`) - Working mode (1 = Low, 2 = High)
- **Ping** (`ping`) - Ping to pool (ms)

### Status Flags
- **Working Status** (`workingstatus`) - Working status ("1" = Fine)

---

## 3. Version Command Data (`version`)

### Product Information
- **PROD / HwType** (`prod`, `hwtype`) - Product name (e.g., "Avalon Nano3s")
- **HWTYPE** (`hwtype`) - Hardware type (e.g., "N_MM1v1_X1")

### Version Numbers
- **LVERSION / Version / FwVer** (`version`, `fw_ver`) - Firmware version
- **API** (`api`) - API version number
- **Compiler** (`compiler`) - Compiler version
- **Type** (`type`) - Type identifier

### Device Identifiers
- **MAC** (`mac`) - MAC address

### Fields Parsed But Not Stored
- MODEL
- SWTYPE

---

## 4. Pools Command Data (`pools`)

### Pool 0 (Primary Pool) - Connection Info
- **URL / Address / PoolUrl / Pool1** (`address`, `pool_url`, `pool1`) - Pool connection URL
- **USER / Worker / PoolUser / Worker1** (`worker`, `pool_user`, `worker1`) - Worker/username
- **PASS / PoolPass / Passwd1** (`pool_pass`, `passwd1`) - Pool password
- **STATUS / PoolStatusDetail** (`pool_status_detail`) - Pool status (Alive, Dead, Disabled)
- **PoolStatus** (`pool_status`) - Pool status ("1" = Connected)
- **PRIORITY / PoolPriority** (`pool_priority`) - Pool priority (0 = highest)
- **QUOTA / PoolQuota** (`pool_quota`) - Pool quota/weight

### Pool 0 - Statistics
- **ACCEPTED / PoolAccepted** (`pool_accepted`) - Accepted shares from this pool
- **REJECTED / PoolRejected** (`pool_rejected`) - Rejected shares from this pool
- **STALE / PoolStale** (`pool_stale`) - Stale shares from this pool
- **DIFF / PoolDiff** (`pool_diff`) - Pool difficulty setting
- **LAST SHARE TIME / PoolLastShareTime** (`pool_last_share_time`) - Timestamp of last share submitted
- **GET FAILURES / PoolGetFailures** (`pool_get_failures`) - Getwork failures
- **REMOTE FAILURES / PoolRemoteFailures** (`pool_remote_failures`) - Remote connection failures
- **POOL BEST SHARE / PoolBestShare** (`pool_best_share`) - **Best share found from this pool** ⚠️ Currently showing as 0

### Pool 0 - Status
- **STRATUM ACTIVE** (`pool_status`) - Stratum connection active (sets PoolStatus to "1" if true)
- **CurrentPool** (`current_pool`) - Current pool number ("1" = pool 0)

### Pool 1 & Pool 2 (Backup Pools)
- **Pool2 / Pool3** (`pool2`, `pool3`) - Pool URLs for backup pools
- **Worker2 / Worker3** (`worker2`, `worker3`) - Worker names for backup pools
- **Passwd2 / Passwd3** (`passwd2`, `passwd3`) - Passwords for backup pools

### Fields Parsed But Not Stored
- CURRENT BLOCK HEIGHT

---

## Calculated/Inferred Fields

### Status Fields (Set Based on Data)
- **AsicStatus** (`asic_status`) - Set to "0" (Fine) if hashrate > 0
- **PowerStatus** (`power_status`) - Set to "0" (Fine) if power > 0
- **SysStatus** (`sys_status`) - System status

---

## Current Issue: Pool Best Share

**Problem**: `PoolBestShare` is always showing as 0 (0.00M)

**Possible Causes**:
1. The field name in the API response might be different (e.g., "Best Share" instead of "Pool Best Share")
2. The field might be in a different section (summary vs pools)
3. The field might not be present in the pools response
4. The parsing might be case-sensitive or have different spacing

**Debug Steps**:
- Check the raw pools response in console logs: `[DEBUG] Raw pools response: ...`
- Verify if "POOL BEST SHARE" or "BEST SHARE" appears in the response
- Check if the value is in the summary response instead of pools response

---

## Summary

**Total Fields Collected**: ~60+ data points
**Main Categories**:
- Hashrate (real-time, average, historical)
- Temperature (operating, max, average)
- Shares (accepted, rejected, stale)
- Pool information (connection, statistics)
- System info (version, MAC, hardware type)
- Power consumption
- Fan speed
- Difficulty metrics

