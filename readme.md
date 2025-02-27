# OTP-Based Authentication System

## Overview
The OTP-Based Authentication System provides a secure method for user authentication using a one-time password (OTP). It ensures that users can verify their identity by entering an OTP sent via email or SMS.

## Features
- Secure user authentication using OTP
- Supports SMS and email-based OTP delivery
- Configurable OTP expiration time
- Resend OTP functionality
- Rate limiting to prevent brute force attacks

## Installation
### Prerequisites
- Python 3.x
- Flask (for backend API)
- Twilio API (for SMS OTPs) or SMTP server (for email OTPs)
- Redis (for OTP storage, optional but recommended)

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/otp-auth-system.git
   cd otp-auth-system
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Set up environment variables:
   ```bash
   export TWILIO_ACCOUNT_SID='your_twilio_sid'
   export TWILIO_AUTH_TOKEN='your_twilio_auth_token'
   export TWILIO_PHONE_NUMBER='your_twilio_phone_number'
   export SMTP_SERVER='your_smtp_server'
   export SMTP_PORT='your_smtp_port'
   export SMTP_USER='your_email'
   export SMTP_PASSWORD='your_email_password'
   ```
4. Run the server:
   ```bash
   python app.py
   ```

## API Endpoints
### 1. Generate OTP
**POST /generate-otp**
#### Request Body
```json
{
  "phone": "+1234567890"
  // OR
  "email": "user@example.com"
}
```
#### Response
```json
{
  "message": "OTP sent successfully",
  "otp_id": "unique_otp_identifier"
}
```

### 2. Verify OTP
**POST /verify-otp**
#### Request Body
```json
{
  "otp_id": "unique_otp_identifier",
  "otp": "123456"
}
```
#### Response
```json
{
  "message": "OTP verified successfully",
  "token": "jwt_access_token"
}
```

## Configuration
- `OTP_LENGTH`: Length of OTP (default: 6 digits)
- `OTP_EXPIRY`: Expiry time in seconds (default: 300s or 5 mins)
- `MAX_OTP_ATTEMPTS`: Maximum allowed attempts per OTP

## Security Measures
- **Rate Limiting**: Limits OTP requests per user to prevent abuse
- **Expiration & Retry Limits**: OTPs expire after a set time and have a maximum number of attempts
- **Encryption**: OTPs are hashed before storage
- **JWT Token**: After successful OTP verification, a JWT token is issued for session management

## License
This project is licensed under the MIT License.

## Contact
For any issues or suggestions, please open an issue on GitHub or contact .

