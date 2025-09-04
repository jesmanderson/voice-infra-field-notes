# SOP: Integrating Poly CCX 400 SIP Devices with Cisco Unified Communications Manager (CUCM)

## Overview
This Standard Operating Procedure (SOP) provides a structured and repeatable method for registering Poly CCX 400 SIP devices to Cisco Unified Communications Manager (CUCM). These devices are treated as Third-Party SIP Device (Advanced) endpoints within CUCM. The goal is to ensure consistent provisioning, reduce configuration errors, and streamline future onboarding of similar devices.

## Pre-Requirements 
Before beginning, ensure the following are in place:

- CUCM Administrative Access: Required to configure devices and users.
- Poly CCX 400 Device: Powered on and connected to the network.
- Assigned Phone Number: For directory and dialing purposes.
- Digest User (End User): Must be created in CUCM for SIP authentication.
- Firmware: Ensure the Poly device is running compatible firmware.

## Step-by-Step Instructions 
1. **Clone an Existing SIP Phone Profile**
    - Navigate to Device > Phone in CUCM.
    - Locate a working Poly CCX 400 SIP device.
    - Use the Copy function to duplicate the configuration. <br/>

    *Tip: Ensure that Calling Search Space (CSS) and Partitions match the working configuration to avoid call routing issues.*


2. **Create or Update the End User (Digest User)** 
    - Go to User Management > End User.
    - Create a new user or update an existing one.
    - This user will be used for SIP Digest Authentication.

3. **Finalize Phone Configuration in CUCM**
    - Assign the Owner User ID to the Digest User created above.
    - Under Protocol Specific Information, verify:
        - SIP Digest Authentication is enabled.
        - A valid SIP Profile is applied.

4. **Access the Poly Device Web Interface**
    - Connect the phone to the network and allow it to obtain an IP address via DHCP.
    - From a PC, open a browser and navigate to:
        - https://(Phone IP Address)
        - Login credentials (default unless changed):
            - Username: admin
            - Password: default

5. **Configure via Poly Web GUI** 
    - Navigate to Simple Setup.
    - Enter the required SIP credentials and CUCM server details.
    - Save the configuration and reboot the device.

6. **Registration Success**
    - In CUCM, confirm the phone status shows Registered.
    - Place a test call to validate functionality.

## Expected Outcomes
- A clear and repeatable SOP for onboarding Poly CCX 400 devices.
- Reduced configuration errors and faster deployment.
- Easier troubleshooting and scalability for future device additions.

## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)