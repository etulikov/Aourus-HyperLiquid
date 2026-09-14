# Tables and calibrated parameters

## Section 6 — CDX application parameters

The paper treats the theoretical assets as `$1` of each index when stating the price-process and intensity parameters.

| Parameter | CDX.NA.IG | CDX.NA.HY | Notes |
|---|---:|---:|---|
| Volatility `\sigma` | `5.83 × 10^-6 $·s^-1/2` | `2.15 × 10^-5 $·s^-1/2` | Estimated from mid-prices |
| Correlation `\rho` | `0.9` | `0.9` | Cross-index correlation |
| Intensity scale `A` | `9.10 × 10^-4 s^-1` | `1.06 × 10^-3 s^-1` | Exponential-intensity fit |
| Intensity decay `k` | `1.79 × 10^4 $^-1` | `5.47 × 10^3 $^-1` | Exponential-intensity fit |
| Trade size `\Delta` | `$50 million` | `$10 million` | Size used in the numerical application |
| Inventory limit | `Q_IG / \Delta_IG = 4` | `Q_HY / \Delta_HY = 4` | Four trade units each side |

Common parameters:

| Parameter | Value |
|---|---:|
| Reference risk aversion `\gamma` | `6 × 10^-5 $^-1` |
| Horizon `T` | `7200 s` (2 hours) |
| Intensity form | `\Lambda(\delta)=A e^{-k\delta}` |
| Estimation period | First semester of 2016 |

The paper reports that the asymptotic quote regime is reached in far less than the full two-hour horizon, approximately within an hour for both indices.
