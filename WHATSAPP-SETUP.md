# 📱 WhatsApp Integration Setup Guide

## 🎯 What This Does

**EXACTLY what you wanted:**
- User types message in **live chat** → You get it on **WhatsApp**
- You reply from **WhatsApp** → User sees it in **live chat**
- **Real-time bidirectional messaging** between website and WhatsApp

## 🚀 How It Works

### **User Experience:**
1. User opens live chat on website
2. Types message: "I need help with my order"
3. **Message sent to your WhatsApp instantly**
4. You reply from WhatsApp: "Sure! What's your order number?"
5. **User sees your reply in live chat immediately**

### **Your Experience:**
1. Get instant WhatsApp notifications when users message
2. Reply directly from WhatsApp (like normal chat)
3. All messages sync to live chat automatically
4. Full conversation history maintained

## 🛠️ Setup Steps

### **Step 1: WhatsApp Business API Setup**

#### **Option A: Meta Business (Official)**
1. Go to [Meta for Developers](https://developers.facebook.com/)
2. Create app → Business → WhatsApp
3. Get your:
   - `WHATSAPP_ACCESS_TOKEN`
   - `PHONE_NUMBER_ID`
   - `WEBHOOK_VERIFY_TOKEN`

#### **Option B: WhatsApp Cloud API**
1. Go to [WhatsApp Business Platform](https://business.whatsapp.com/products/platform)
2. Sign up for Cloud API
3. Get API credentials

### **Step 2: Deploy the Server**

#### **Option A: Node.js (Recommended)**
```bash
# Install dependencies
npm install

# Set environment variables
export WHATSAPP_ACCESS_TOKEN="your_token_here"
export PHONE_NUMBER_ID="your_phone_id_here" 
export WEBHOOK_VERIFY_TOKEN="shopeasy_webhook_token_2024"

# Start server
npm start
```

#### **Option B: PHP**
```bash
# Upload whatsapp-webhook.php to your server
# Configure variables in the PHP file
# Set webhook URL in Meta console
```

### **Step 3: Configure Webhook**

1. **In Meta Developer Console:**
   - Webhook URL: `https://yourdomain.com/webhook`
   - Verify Token: `shopeasy_webhook_token_2024`
   - Subscribe to: `messages`

2. **Test webhook:**
```bash
curl -X GET "https://yourdomain.com/webhook?hub.mode=subscribe&hub.verify_token=shopeasy_webhook_token_2024&hub.challenge=test123"
```

### **Step 4: Update Your Website**

Add to your website's JavaScript:
```javascript
// Enable WhatsApp integration
localStorage.setItem('whatsappIntegrationEnabled', 'true');
localStorage.setItem('adminWhatsAppNumber', 'YOUR_WHATSAPP_NUMBER');
```

## 📋 Configuration Files

### **Environment Variables (.env)**
```env
# WhatsApp API Configuration
WHATSAPP_ACCESS_TOKEN=your_access_token_here
PHONE_NUMBER_ID=your_phone_number_id_here
WEBHOOK_VERIFY_TOKEN=shopeasy_webhook_token_2024

# Server Configuration
PORT=3000
NODE_ENV=production
```

### **Server Configuration**
Update `whatsapp-server.js`:
```javascript
// Replace YOUR_WHATSAPP_NUMBER with your actual WhatsApp number
const ADMIN_WHATSAPP = "+1234567890"; // Your WhatsApp number
```

## 🧪 Testing

### **Test Message Flow:**
1. **Website → WhatsApp:**
   - Type message in live chat
   - Check your WhatsApp for notification
   - Message should include user info and session ID

2. **WhatsApp → Website:**
   - Reply to the WhatsApp message
   - Check live chat for your reply
   - Should appear with WhatsApp icon

### **Debug Commands:**
```bash
# Check server health
curl https://yourdomain.com/health

# Check webhook
curl https://yourdomain.com/webhook

# Test message API
curl -X POST https://yourdomain.com/api/send-message \
  -H "Content-Type: application/json" \
  -d '{"to":"+1234567890","message":"Test message"}'
```

## 🔧 API Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/webhook` | GET | Webhook verification |
| `/webhook` | POST | Receive WhatsApp messages |
| `/api/messages` | GET | Get chat messages |
| `/api/send-message` | POST | Send message to WhatsApp |
| `/api/conversations` | GET | Get active conversations |
| `/health` | GET | Server health check |

## 📱 Message Format

### **Website → WhatsApp:**
```
🛍️ ShopEasy Live Chat Message

👤 Customer: John Doe
📧 Email: john@example.com
🆔 Session: chat_1704384921000
🕒 Time: 1/4/2024, 3:22:01 PM

💬 Message:
I need help with my order

Sent from ShopEasy website live chat
Reply to this message to respond to customer
```

### **WhatsApp → Website:**
```
📱 Admin replied via WhatsApp:

Hi! I can help you with your order. What's your order number?
```

## 🚨 Troubleshooting

### **Common Issues:**

#### **"Webhook verification failed"**
- Check `WEBHOOK_VERIFY_TOKEN` matches in both places
- Ensure webhook URL is accessible
- Verify HTTPS is working

#### **"Messages not forwarding"**
- Check `WHATSAPP_ACCESS_TOKEN` is valid
- Verify `PHONE_NUMBER_ID` is correct
- Check server logs for errors

#### **"Replies not showing in chat"**
- Ensure website can access `/api/messages`
- Check browser console for errors
- Verify WhatsApp integration is enabled

### **Debug Steps:**
1. Check server logs: `tail -f logs/app.log`
2. Test webhook: `curl https://yourdomain.com/webhook`
3. Check API: `curl https://yourdomain.com/api/messages`
4. Verify WhatsApp API: Check Meta Developer Console

## 🎯 Deployment Options

### **Option 1: Heroku**
```bash
git clone your-repo
cd your-repo
heroku create your-app-name
heroku config:set WHATSAPP_ACCESS_TOKEN=your_token
heroku config:set PHONE_NUMBER_ID=your_phone_id
git push heroku main
```

### **Option 2: Vercel**
```bash
vercel --prod
vercel env add WHATSAPP_ACCESS_TOKEN
vercel env add PHONE_NUMBER_ID
```

### **Option 3: DigitalOcean/AWS/VPS**
```bash
# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Clone and setup
git clone your-repo
cd your-repo
npm install
npm start
```

## ✅ Success Checklist

- [ ] WhatsApp Business API account created
- [ ] Server deployed and running
- [ ] Webhook verified and configured
- [ ] Environment variables set
- [ ] Test message sent website → WhatsApp
- [ ] Test reply sent WhatsApp → website
- [ ] Integration enabled on website
- [ ] Admin WhatsApp number configured

## 🎉 Ready to Use!

Once setup is complete:

1. **Users message on website** → **You get WhatsApp notification**
2. **You reply on WhatsApp** → **Users see reply in live chat**
3. **Perfect real-time integration!**

**Support:** If you need help, contact via the live chat on the website! 😄

---

## 📞 Contact Information

- **Website:** https://ctrlxmir.github.io/reactify-mir/
- **GitHub:** https://github.com/ctrlXmir/reactify-mir
- **Issues:** Open GitHub issue for technical support

**Happy messaging! 🚀📱💬**