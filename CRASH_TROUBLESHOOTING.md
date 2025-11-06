# 🆘 App Crash Troubleshooting Guide

## 🔍 Step 1: Run the Diagnostic Tool

```bash
python diagnose.py
```

This will check:
- ✅ Python version
- ✅ Required packages
- ✅ File syntax errors  
- ✅ Common issues

## 📋 Common Crash Causes & Solutions

### ❌ Crash #1: "ModuleNotFoundError: No module named 'streamlit'"
**Cause:** Missing dependencies

**Solution:**
```bash
pip install streamlit pandas numpy requests pytz scikit-learn
```

Or use the setup script:
```bash
chmod +x setup.sh
./setup.sh
```

---

### ❌ Crash #2: "NameError: name 'american_to_decimal_safe' is not defined"
**Cause:** Using old buggy version

**Solution:** Use the fixed version
```bash
# Use this instead:
streamlit run streamlit_app_enhanced_v2.py
```

---

### ❌ Crash #3: "OSError: [Errno 30] Read-only file system: '/home/claude/historical_cache'"
**Cause:** Path issue (was hardcoded for my environment)

**Solution:** Already fixed in `streamlit_app_enhanced_v2.py`
```bash
streamlit run streamlit_app_enhanced_v2.py
```

---

### ❌ Crash #4: App starts then immediately crashes
**Cause:** Streamlit version too old

**Solution:**
```bash
pip install --upgrade streamlit
```

---

### ❌ Crash #5: "AttributeError: module 'sklearn' has no attribute..."
**Cause:** scikit-learn not installed or too old

**Solution:**
```bash
pip install --upgrade scikit-learn
```

---

### ❌ Crash #6: API errors during training
**Cause:** API key issues or quota exceeded

**Solution:**
1. Check your API key at https://the-odds-api.com/account/
2. Verify you have historical data access
3. Check your API quota
4. Try with fewer days (e.g., 7-14 days instead of 90)

---

## 🎯 Which File Should You Run?

### Use `streamlit_app_enhanced_v2.py` ⭐ (LATEST, MOST STABLE)
- ✅ Fixed all path issues
- ✅ Better error handling
- ✅ Works on any operating system
- ✅ Graceful degradation if ML not available

```bash
streamlit run streamlit_app_enhanced_v2.py
```

### Use `streamlit_app.py` (BASIC VERSION)
- ✅ No ML training needed
- ✅ Works with basic API subscription
- ✅ Good for testing

```bash
streamlit run streamlit_app.py
```

### DON'T use `streamlit_app_enhanced.py` (OLD VERSION)
- ❌ Has hardcoded paths that won't work
- Use `streamlit_app_enhanced_v2.py` instead

---

## 🐛 Debugging Steps

### 1. Check Terminal Output
When the app crashes, look at your terminal. The error message tells you what's wrong:

```
ModuleNotFoundError: No module named 'sklearn'
→ Solution: pip install scikit-learn

NameError: name 'american_to_decimal_safe' is not defined
→ Solution: Use the fixed file

FileNotFoundError: [Errno 2] No such file or directory: '/home/claude/...'
→ Solution: Use streamlit_app_enhanced_v2.py
```

### 2. Run Diagnostic Tool
```bash
python diagnose.py
```

Look for ❌ marks and follow the instructions.

### 3. Test Basic Functionality
```bash
python -c "import streamlit; print('Streamlit OK')"
python -c "import pandas; print('Pandas OK')"
python -c "import sklearn; print('Scikit-learn OK')"
```

All should print "OK" without errors.

### 4. Check Package Versions
```bash
pip list | grep streamlit
pip list | grep scikit-learn
```

Required versions:
- streamlit >= 1.28.0
- scikit-learn >= 1.3.0

---

## 💡 Quick Fix Guide

### If you see this error...

**"No module named 'X'"**
```bash
pip install X
```

**"american_to_decimal_safe is not defined"**
```bash
# Use the v2 file
streamlit run streamlit_app_enhanced_v2.py
```

**"Read-only file system"**
```bash
# Use the v2 file (fixed paths)
streamlit run streamlit_app_enhanced_v2.py
```

**"API request failed"**
- Check your API key
- Verify internet connection
- Check https://the-odds-api.com/status/

**"ML libraries not installed"**
```bash
pip install scikit-learn
```

---

## 🎯 Step-by-Step Fresh Start

If nothing works, try this complete reset:

```bash
# 1. Uninstall everything
pip uninstall streamlit pandas numpy requests pytz scikit-learn -y

# 2. Reinstall fresh
pip install streamlit pandas numpy requests pytz scikit-learn

# 3. Run diagnostic
python diagnose.py

# 4. Run the latest version
streamlit run streamlit_app_enhanced_v2.py
```

---

## 📱 Share Error Details

If still crashing, share these details:

1. **Full error message** from terminal (copy-paste everything)
2. **Which file** you're running
3. **Python version**: `python --version`
4. **Streamlit version**: `pip show streamlit`
5. **When it crashes**: On startup? After clicking button? During training?

### How to capture the error:

```bash
# Run with full error output
streamlit run streamlit_app_enhanced_v2.py 2>&1 | tee error.log
```

This saves the error to `error.log` which you can share.

---

## ✅ Expected Successful Startup

When working correctly, you should see:

```
  You can now view your Streamlit app in your browser.

  Local URL: http://localhost:8501
  Network URL: http://192.168.x.x:8501
```

The app should open in your browser showing:
- 🎯 Title: "ParlayDesk - AI-Enhanced Odds Finder"
- Sidebar with API key input
- Three tabs: AI Parlay Finder, PrizePicks, Historical Analysis

---

## 🆘 Still Not Working?

### Try the basic version first:
```bash
streamlit run streamlit_app.py
```

If this works but the enhanced version doesn't, it's likely:
- scikit-learn not installed → `pip install scikit-learn`
- API issues → Check historical data access

### Get help:
1. Run `python diagnose.py` and share output
2. Copy the full terminal error
3. Check which Python you're using: `which python`
4. Verify you're in the right directory: `ls -la`

---

## 🎓 Testing Without API Key

You can test the app loads correctly even without an API key:

```bash
streamlit run streamlit_app_enhanced_v2.py
```

You should see:
- App loads successfully ✅
- Shows "⚠️ Please enter your Odds API key" ✅
- No crashes ✅

If it crashes before showing the API key input, that's a package/syntax error.

---

## 🔄 File Version Summary

| File | Status | Use For |
|------|--------|---------|
| `streamlit_app.py` | ✅ Fixed | Basic odds, no ML |
| `streamlit_app_enhanced.py` | ❌ OLD | Don't use (path bugs) |
| `streamlit_app_enhanced_v2.py` | ✅ LATEST | ML with historical data |
| `diagnose.py` | ✅ Tool | Finding crash causes |

**Always use `streamlit_app_enhanced_v2.py` for the ML version!**

---

Need more help? Share:
1. Output from `python diagnose.py`
2. Full error message from terminal
3. What you tried already

Good luck! 🍀
