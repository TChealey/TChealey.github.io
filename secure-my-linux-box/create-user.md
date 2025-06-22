# Create a Non-root Sudo User in RHEL

**Purpose:**
To create a new user account with administrative (sudo) privileges on a RHEL system to avoid using the root user directly.

## Commands Used

'''bash
add user tawana
password tawana
usermod -aGwheel tawana
id tawana

Confirmed user creation with: 'id tawana'
Verified membership in the 'wheel' group for sudo access
