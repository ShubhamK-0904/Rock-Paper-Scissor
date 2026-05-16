# 📞 Phone Number Detail Tracker

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Phone%20Tracking-FF6B6B?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Geocoding-4285F4?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" />
</p>

---

## 📋 Overview

**Phone Number Detail Tracker** is a Python project using Google's `phonenumbers` library (libphonenumber) to parse and track phone number details. Provides country-based location, carrier name, timezone information, and comprehensive phone number validation, demonstrating modules like Geocoder, Carrier, and Timezone for international telecommunications.

**Perfect for:** Learning phone number validation, geo-location tracking, international dialing, telecom data analysis.

---

## ✨ Key Features

- 🌍 **Location Detection**
  - Country identification
  - Region/State extraction
  - Geographic coordinates
  - Time zone mapping

- 📱 **Carrier Information**
  - Carrier name detection
  - Operator identification
  - Service provider details
  - Network type classification

- ⏰ **Timezone Analysis**
  - Timezone extraction
  - UTC offset calculation
  - DST handling
  - Time zone mapping

- ✔️ **Number Validation**
  - Format validation
  - Number type detection
  - International format support
  - E.164 standardization

- 🔍 **Advanced Analysis**
  - Mobile vs landline detection
  - SMS capability check
  - Call forwarding detection
  - Number portability status

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Language** | Python 3.8+ |
| **Core Library** | phonenumbers (libphonenumber) |
| **Geocoding** | Google's geocoder module |
| **Carrier Detection** | Carrier module |
| **Timezone** | Timezone module |

---

## 📋 Requirements

```bash
pip install phonenumbers
```

---

## 🚀 Quick Start

### 1. **Clone Repository**
```bash
git clone https://github.com/ShubhamK-0904/Phno_Detailtracker.git
cd Phno_Detailtracker
```

### 2. **Install Dependencies**
```bash
pip install phonenumbers
```

### 3. **Run Tracker**
```bash
python phone_tracker.py
```

---

## 💻 Usage Examples

### **1. Basic Phone Number Parsing**
```python
import phonenumbers

# Parse phone number
number = phonenumbers.parse("+91 98765 43210", "IN")
print(f"Valid: {phonenumbers.is_valid_number(number)}")
print(f"E.164 Format: {phonenumbers.format_number(number, phonenumbers.PhoneNumberFormat.E164)}")
```

### **2. Get Location Information**
```python
import phonenumbers
from phonenumbers import geocoder

number = phonenumbers.parse("+1 202 555 0173", None)
location = geocoder.description_for_number(number, "en")
print(f"Location: {location}")
```

### **3. Get Carrier Information**
```python
import phonenumbers
from phonenumbers import carrier

number = phonenumbers.parse("+91 98765 43210", None)
carrier_name = carrier.name_for_number(number, "en")
print(f"Carrier: {carrier_name}")
```

### **4. Get Timezone Information**
```python
import phonenumbers
from phonenumbers import timezone

number = phonenumbers.parse("+1 202 555 0173", None)
timezones = timezone.time_zones_for_number(number)
print(f"Timezones: {timezones}")
```

### **5. Comprehensive Phone Analysis**
```python
import phonenumbers
from phonenumbers import geocoder, carrier, timezone

def analyze_phone(phone_str, country=None):
    try:
        number = phonenumbers.parse(phone_str, country)
        
        # Validation
        is_valid = phonenumbers.is_valid_number(number)
        is_possible = phonenumbers.is_possible_number(number)
        
        # Type detection
        number_type = phonenumbers.number_type(number)
        
        # Location
        location = geocoder.description_for_number(number, "en")
        
        # Carrier
        carrier_name = carrier.name_for_number(number, "en")
        
        # Timezone
        timezones = timezone.time_zones_for_number(number)
        
        return {
            'Valid': is_valid,
            'Possible': is_possible,
            'Type': number_type,
            'Location': location,
            'Carrier': carrier_name,
            'Timezone': timezones,
            'E164': phonenumbers.format_number(number, phonenumbers.PhoneNumberFormat.E164)
        }
    except phonenumbers.NumberParseException as e:
        return {'Error': str(e)}

result = analyze_phone("+91 98765 43210")
for key, value in result.items():
    print(f"{key}: {value}")
```

### **6. Batch Phone Tracking**
```python
import phonenumbers
from phonenumbers import geocoder, carrier

def batch_analyze(phone_list):
    results = []
    for phone in phone_list:
        try:
            number = phonenumbers.parse(phone, None)
            location = geocoder.description_for_number(number, "en")
            carrier_name = carrier.name_for_number(number, "en")
            
            results.append({
                'Phone': phone,
                'Valid': phonenumbers.is_valid_number(number),
                'Location': location,
                'Carrier': carrier_name
            })
        except Exception as e:
            results.append({'Phone': phone, 'Error': str(e)})
    
    return results

phones = ["+91 98765 43210", "+1 202 555 0173", "+44 20 7946 0958"]
analysis = batch_analyze(phones)
for result in analysis:
    print(result)
```

---

## 🎯 Number Types

| Type | Description |
|------|-------------|
| **MOBILE** | Mobile phone number |
| **FIXED_LINE** | Landline number |
| **FIXED_LINE_OR_MOBILE** | Could be either |
| **TOLL_FREE** | Toll-free number |
| **PREMIUM_RATE** | Premium service |
| **SHARED_COST** | Shared cost |
| **VOIP** | VoIP number |
| **PERSONAL_NUMBER** | Personal number |
| **PAGER** | Pager number |
| **UAN** | Universal access number |
| **VOICEMAIL** | Voicemail number |

---

## 📊 Supported Regions

- ✅ All countries (200+)
- ✅ International dialing codes
- ✅ Country-specific formats
- ✅ Regional variations
- ✅ Special number types

---

## 🔍 Information You Can Extract

### **Personal Information**
```
- Country
- Region/State
- City
- Area code
- Timezone
```

### **Service Information**
```
- Carrier/Operator
- Number type (mobile/landline)
- SMS capability
- International roaming support
```

### **Format Options**
```
E164:        +1 2025550173
INTERNATIONAL: +1 202-555-0173
NATIONAL:    (202) 555-0173
RFC3966:     tel:+1-202-555-0173
```

---

## 💡 Real-World Applications

✅ **Contact Verification:** Validate customer phone numbers  
✅ **Spam Detection:** Identify suspicious numbers  
✅ **Location Services:** Geo-locate callers  
✅ **Billing Systems:** Carrier-based routing  
✅ **CRM Integration:** Auto-populate customer data  
✅ **Communication Apps:** Format international numbers  
✅ **Telecom Analytics:** Track carrier distribution  

---

## 🎓 Learning Outcomes

Master these concepts:
- ✅ Phone number standards (E.164, ITU)
- ✅ International dialing codes
- ✅ Carrier and telecom data
- ✅ Geocoding techniques
- ✅ Data parsing and validation
- ✅ Batch processing

---

## 📊 Project Stats

| Metric | Value |
|--------|-------|
| **Supported Countries** | 200+ |
| **Number Types** | 11 |
| **Format Types** | 4+ |
| **Timezone Support** | Full |

---

## 🚀 Future Enhancements

- [ ] Web API endpoint
- [ ] GUI application
- [ ] Database storage
- [ ] Real-time SMS tracking
- [ ] Call detail records analysis
- [ ] International roaming detection
- [ ] Number porting status
- [ ] Fraud detection integration

---

## 🤝 Contributing

Contributions welcome!
1. Fork repository
2. Create feature branch
3. Add improvements
4. Submit pull request

---

## 📝 License

MIT License - see LICENSE file

---

## 👨‍💻 Author

**Shubham Kadam**
- GitHub: [@ShubhamK-0904](https://github.com/ShubhamK-0904)
- LinkedIn: [Shubham Kadam](https://www.linkedin.com/in/shubham-kadam-b8856031a/)
- Email: shubham85kadam@gmail.com

---

<p align="center">
  <strong>⭐ If helpful, give it a star! ⭐</strong>
</p>

<p align="center">
  Made with ❤️ by Shubham Kadam | Last Updated: May 2026
</p>
