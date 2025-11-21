# Partnership UI Automation

UI automation test suite for **Mint Portfolio powered by Dezerv** mobile application using Maestro framework.

## Overview

This project contains end-to-end UI automation tests for the Mint Portfolio mobile app (`com.htmedia.mint`). The test suite validates critical user flows including login, portfolio tracking (Mutual Funds, Stocks, Banks), FAQ sections, daily movement tracking, and expert call booking.

## Technology Stack

- **Framework**: [Maestro](https://maestro.mobile.dev/) - Mobile UI testing framework
- **Test Format**: YAML-based test definitions
- **Target App**: Mint Portfolio (`com.htmedia.mint`)
- **Platform**: Android

## Project Structure

```
Partneship-UI-Automation-workspace/
├── run.sh                    # Main execution script
├── scripts/
│   └── set_flag.sh          # Sets automation flag on Android device
├── Tests/
│   ├── E2E/
│   │   └── end-to-end.yaml  # Complete end-to-end test suite
│   ├── Features/            # Feature-based test flows
│   │   ├── 1_Login.yaml
│   │   ├── 2_FAQ.yaml
│   │   ├── 3_MF.yaml
│   │   ├── 4_Stocks.yaml
│   │   ├── 5_Banks.yaml
│   │   ├── 6_DailyMovement.yaml
│   │   └── Runner.yaml      # Feature test runner
│   └── Pages/               # Page tests
│       ├── 0_login.yaml
│       ├── 1_HomePage.yaml
│       ├── 2-7_FAQ_*.yaml   # FAQ page objects
│       ├── 8-11_MF_*.yaml   # Mutual Funds page objects
│       ├── 12-14_Stocks_*.yaml
│       ├── 15-16_Banks_*.yaml
│       ├── 17-20_DailyMovement_*.yaml
│       ├── 21_Expert_Call.yaml
│       └── Runner.yaml        # Page test runner
└── wait.yaml                # Wait configuration
```

## Prerequisites

1. **Maestro CLI**: Install Maestro framework
   ```bash
   curl -Ls "https://get.maestro.mobile.dev" | bash
   ```

2. **Android Device/Emulator**: 
   - Android device connected via ADB, or
   - Android emulator running

3. **ADB (Android Debug Bridge)**: Ensure ADB is installed and device is connected
   ```bash
   adb devices
   ```

4. **App Installation**: The Mint app (`com.htmedia.mint`) should be installed on the target device

## Setup

1. **Clone the repository** (if applicable)

2. **Navigate to the workspace directory**:
   ```bash
   cd Partneship-UI-Automation-workspace
   ```

3. **Ensure the device is connected**:
   ```bash
   adb devices
   ```

4. **Make scripts executable** (if needed): Open terminal at Scipts folder and execute below commands
   ```bash
   chmod +x run.sh
   chmod +x scripts/set_flag.sh
   ```

## Running Tests

### Run All Feature Tests (via Runner)
   ```bash
maestro test Tests/Pages/Runner.yaml
   ```

### Run All Feature Tests (via Runner)
   ```bash
maestro test Tests/Features/Runner.yaml
   ```

### Run All end-to-end test suite Tests
   ```bash
maestro test Tests/E2E/end-to-end.yaml
   ```

### Run Individual Tests
   ```bash
maestro test Tests/Pages/0_Login.yaml
   ```   
      ```bash
maestro test Tests/Features/2_FAQ.yaml
   ``` 

This script will:
1. Set the automation flag on the Android device
2. Run the login test flow

## Test Coverage

### 1. **Login Flow** (`1_Login.yaml`)
- App launch and onboarding
- Phone number entry and OTP verification
- Home page validation

### 2. **FAQ Tests** (`2_FAQ.yaml`)
- General FAQs
- Privacy & Security FAQs
- Bank-related FAQs
- Mutual Fund FAQs
- Stock-related FAQs
- Data Sharing & Consent management

### 3. **Mutual Funds** (`3_MF.yaml`)
- MF header and summary validation
- Holdings list and details
- Portfolio performance metrics
- Fund analysis and insights

### 4. **Stocks** (`4_Stocks.yaml`)
- Stock holdings header
- Portfolio analysis and summary
- Holdings list
- Performance tracking

### 5. **Banks** (`5_Banks.yaml`)
- Bank account analysis
- Transaction history and filters
- Cash flow summary
- Account management

### 6. **Daily Movement** (`6_DailyMovement.yaml`)
- Daily returns tracking for MF and Stocks
- Movement via Home screen
- Movement via L1 detail screens

### 7. **Expert Call** (`21_Expert_Call.yaml`)
- Expert call booking flow
- Slot selection and confirmation

## Scripts

### `scripts/set_flag.sh`
Sets an automation flag on the Android device:
```bash
adb shell "echo true > /data/local/tmp/is_automation"
```

This flag is used by the app to identify automation test runs.

## Configuration

### App ID
The target app ID is configured in each test file:
```yaml
appId: com.htmedia.mint
```

### Test Data
- **Phone Number**: `1133557799` (configured in login flow)
- **OTP**: `3344` (test OTP value)

**Note**: Update these values as needed for your test environment.

## Page Objects

The Pages are reusable page object definitions:
- Login page interactions
- Home page validations
- FAQ page flows
- MF, Stocks, and Banks page objects
- Daily Movement page objects
- Expert Call page objects

## Best Practices

1. **Test Isolation**: Each feature test can run independently
2. **Reusability**: Page objects are defined separately for maintainability
3. **Conditional Flows**: Tests use `runFlow` with `when` conditions for flexible execution
4. **Assertions**: Comprehensive visibility and text assertions validate UI elements
5. **Wait Strategies**: Uses `waitForAnimationToEnd` and delays for stable test execution

## Troubleshooting

### Device Not Detected
```bash
# Check ADB connection
adb devices

# Restart ADB server if needed
adb kill-server
adb start-server
```

### App Not Installed
```bash
# Install the app (if you have the APK)
adb install path/to/app.apk
```

### Automation Flag Issues
```bash
# Manually set the flag
adb shell "echo true > /data/local/tmp/is_automation"

# Verify the flag
adb shell "cat /data/local/tmp/is_automation"
```

### Test Failures
- Ensure the app is in the expected state before running tests
- Check network connectivity for OTP and data sync
- Verify test data (phone number, OTP) matches your test environment
- Review Maestro logs for detailed error messages

## Contributing

When adding new tests:
1. Follow the existing naming convention (`N_FeatureName.yaml`)
2. Update the appropriate Runner file
3. Add page tests in the `Pages/` directory if needed
4. Document any new test data requirements


## Author

Ravikumar - SDET - Partnerships

