# Pkl NHI

A function to check strings against the New Zealand Ministry of Health NHI
Validation Routine.
Supports the old and new NHI number formats specified in
[HISO 10046:2023](https://www.tewhatuora.govt.nz/publications/hiso-100462023-consumer-health-identity-standard/).

## Install

Add the following to your PklProject:

```pkl
dependencies {
  ["nhi"] { 
    uri = "package://pkg.pkl-lang.org/github.com/James-Ansley/pkl-nhi/nhi@0.0.2"
  }
}
```

## Usage

Use the `nhi.isValid` function:

```pkl
import "@nhi/nhi.pkl"

typealias Nhi = String(nhi.isValid(this))

myOtherValidNhi: Nhi = "ZAC5361" // works
myOtherInvalidNhi: Nhi = "ZZZ0044"  // fails
```

Checks are case-insensitive.

***Note:*** This does not check that the NHI number has been _assigned_ to
a person, it merely checks the NHI is consistent with the HISO 10046:2023
standard.

### Excluding Testcases

NHI numbers that begin with `Z` are reserved for testing.
If you wish to exclude these values, you will need to manually check for a `Z`
prefix:

```pkl
import "@nhi/nhi.pkl"

typealias Nhi = String(nhi.isValid(this), !startsWith("Z"), !startsWith("z"))

myNhi1: Nhi = "ABC12AY" // works
myNhi2: Nhi = "ZAC5361"  // fails
```

***Note:*** This check does not mean that the NHI number has been _assigned_ to
a person, it just means that the NHI value is not reserved for testing.

## See Also

- <https://www.tewhatuora.govt.nz/publications/hiso-100462023-consumer-health-identity-standard/>
- <https://www.tewhatuora.govt.nz/our-health-system/digital-health/health-identity/national-health-index/information-for-health-it-vendors-and-developers>
