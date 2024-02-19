# Pkl NHI

A function to check strings against the New Zealand Ministry of Health NHI
Validation Routine.
Supports the old and new NHI number formats specified in
[HISO 10046:2023](https://www.tewhatuora.govt.nz/publications/hiso-100462023-consumer-health-identity-standard/).

## Install

Add the following to you PklProject:

```
dependencies {
  ["nhi"] { uri = "package://github.com/James-Ansley/pkl-nhi/releases/download/v0.0.1/@0.0.1" }
}
```

## Usage

```python
import "@nhi/nhi.pkl"

myValidNhi: String(nhi.isValid(this)) = "ZAC5361"  // works
myInvalidNhi: String(nhi.isValid(this)) = "ZZZ0044"  // fails
```

Checks are case-insensitive.

***Note:*** This does not check that the NHI number has been _assigned_ to
a person, it merely checks the NHI is consistent with the HISO 10046:2023
standard.

### Excluding Testcases

NHI numbers that begin with `Z` are reserved for testing.
If you wish to exclude these values, you will need to manually check for a `Z`
prefix or use the `isReserved`/`isUnreserved` functions:

```python
import "@nhi/nhi.pkl"

myNhi1: String(nhi.isReserved(this) && nhi.isValid(this)) = "ZAC5361" // works
myNhi2: String(nhi.isUnreserved(this) && nhi.isValid(this)) = "ZAC5361"  // fails
```

***Note:*** This check does not mean that the NHI number has been _assigned_ to
a person, it just means that the NHI value is not reserved for testing.

## See Also

- <https://www.tewhatuora.govt.nz/publications/hiso-100462023-consumer-health-identity-standard/>
- <https://www.tewhatuora.govt.nz/our-health-system/digital-health/health-identity/national-health-index/information-for-health-it-vendors-and-developers>
