# n<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Instagram - Reset Password</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .input-field:focus + .input-label,
        .input-field:not(:placeholder-shown) + .input-label {
            transform: translateY(-20px) scale(0.8);
            color: #8e8e8e;
        }
        .password-toggle {
            position: absolute;
            right: 10px;
            top: 50%;
            transform: translateY(-50%);
            cursor: pointer;
            color: #8e8e8e;
        }
        .error-message {
            color: #ed4956;
            font-size: 12px;
            margin-top: 4px;
            display: none;
        }
        .success-message {
            color: #4BB543;
            font-size: 14px;
            margin-top: 10px;
            display: none;
        }
    </style>
</head>
<body class="bg-gray-50 min-h-screen flex items-center justify-center p-4">
    <div class="max-w-md w-full bg-white rounded-lg shadow-sm border border-gray-300 p-8">
        <div class="flex justify-center mb-8">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2a/Instagram_logo.svg/1200px-Instagram_logo.svg.png" alt="Instagram" class="h-12">
        </div>
        
        <div class="text-center mb-6">
            <h1 class="text-xl font-semibold text-gray-800">Reset Your Password</h1>
            <p class="text-gray-500 text-sm mt-2">Enter your current password and set a new one</p>
        </div>
        
        <form id="resetForm" class="space-y-4">
            <div class="relative">
                <input 
                    type="password" 
                    id="currentPassword" 
                    class="input-field w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-gray-500" 
                    placeholder=" "
                    required
                >
                <label for="currentPassword" class="input-label absolute left-3 top-2 text-gray-500 transition-all duration-200 pointer-events-none">Current Password</label>
                <span class="password-toggle" onclick="togglePassword('currentPassword', 'currentToggle')">
                    <i id="currentToggle" class="far fa-eye"></i>
                </span>
                <div id="currentError" class="error-message">Please enter your current password</div>
            </div>
            
            <div class="relative">
                <input 
                    type="password" 
                    id="newPassword" 
                    class="input-field w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-gray-500" 
                    placeholder=" "
                    required
                    minlength="8"
                >
                <label for="newPassword" class="input-label absolute left-3 top-2 text-gray-500 transition-all duration-200 pointer-events-none">New Password</label>
                <span class="password-toggle" onclick="togglePassword('newPassword', 'newToggle')">
                    <i id="newToggle" class="far fa-eye"></i>
                </span>
                <div id="newError" class="error-message">Password must be at least 8 characters</div>
            </div>
            
            <div class="relative">
                <input 
                    type="password" 
                    id="confirmPassword" 
                    class="input-field w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-gray-500" 
                    placeholder=" "
                    required
                >
                <label for="confirmPassword" class="input-label absolute left-3 top-2 text-gray-500 transition-all duration-200 pointer-events-none">Confirm New Password</label>
                <span class="password-toggle" onclick="togglePassword('confirmPassword', 'confirmToggle')">
                    <i id="confirmToggle" class="far fa-eye"></i>
                </span>
                <div id="confirmError" class="error-message">Passwords don't match</div>
            </div>
            
            <div id="successMessage" class="success-message text-center">
                Password changed successfully!
            </div>
            
            <button 
                type="submit" 
                class="w-full bg-blue-500 hover:bg-blue-600 text-white font-medium py-1.5 px-4 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-300 transition duration-200"
                id="submitBtn"
            >
                Reset Password
            </button>
        </form>
        
        <div class="mt-6 text-center">
            <a href="#" class="text-blue-500 text-sm font-medium">Back to login</a>
        </div>
        
        <div class="mt-8 border-t border-gray-300 pt-4 text-center">
            <p class="text-xs text-gray-500">© 2023 Instagram by Meta</p>
        </div>
    </div>

    <script>
        // Toggle password visibility
        function togglePassword(inputId, toggleId) {
            const input = document.getElementById(inputId);
            const toggle = document.getElementById(toggleId);
            
            if (input.type === 'password') {
                input.type = 'text';
                toggle.classList.remove('fa-eye');
                toggle.classList.add('fa-eye-slash');
            } else {
                input.type = 'password';
                toggle.classList.remove('fa-eye-slash');
                toggle.classList.add('fa-eye');
            }
        }
        
        // Form validation
        document.getElementById('resetForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const currentPassword = document.getElementById('currentPassword');
            const newPassword = document.getElementById('newPassword');
            const confirmPassword = document.getElementById('confirmPassword');
            
            const currentError = document.getElementById('currentError');
            const newError = document.getElementById('newError');
            const confirmError = document.getElementById('confirmError');
            
            const successMessage = document.getElementById('successMessage');
            
            let isValid = true;
            
            // Reset error messages
            currentError.style.display = 'none';
            newError.style.display = 'none';
            confirmError.style.display = 'none';
            
            // Validate current password
            if (!currentPassword.value) {
                currentError.textContent = 'Please enter your current password';
                currentError.style.display = 'block';
                isValid = false;
            }
            
            // Validate new password
            if (!newPassword.value) {
                newError.textContent = 'Please enter a new password';
                newError.style.display = 'block';
                isValid = false;
            } else if (newPassword.value.length < 8) {
                newError.textContent = 'Password must be at least 8 characters';
                newError.style.display = 'block';
                isValid = false;
            }
            
            // Validate confirm password
            if (!confirmPassword.value) {
                confirmError.textContent = 'Please confirm your new password';
                confirmError.style.display = 'block';
                isValid = false;
            } else if (newPassword.value !== confirmPassword.value) {
                confirmError.textContent = 'Passwords don\'t match';
                confirmError.style.display = 'block';
                isValid = false;
            }
            
            // If all validations pass
            if (isValid) {
                // Simulate API call
                const submitBtn = document.getElementById('submitBtn');
                submitBtn.disabled = true;
                submitBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Processing...';
                
                setTimeout(() => {
                    successMessage.style.display = 'block';
                    submitBtn.innerHTML = 'Password Changed';
                    submitBtn.classList.remove('bg-blue-500', 'hover:bg-blue-600');
                    submitBtn.classList.add('bg-green-500', 'hover:bg-green-600');
                    
                    // Reset form after success
                    setTimeout(() => {
                        currentPassword.value = '';
                        newPassword.value = '';
                        confirmPassword.value = '';
                        
                        // Reset labels position if empty
                        document.querySelectorAll('.input-field').forEach(input => {
                            if (!input.value) {
                                input.nextElementSibling.style.transform = '';
                            }
                        });
                        
                        successMessage.style.display = 'none';
                        submitBtn.innerHTML = 'Reset Password';
                        submitBtn.disabled = false;
                        submitBtn.classList.remove('bg-green-500', 'hover:bg-green-600');
                        submitBtn.classList.add('bg-blue-500', 'hover:bg-blue-600');
                    }, 2000);
                }, 1500);
            }
        });
        
        // Add floating label effect
        document.querySelectorAll('.input-field').forEach(input => {
            input.addEventListener('focus', function() {
                this.nextElementSibling.style.transform = 'translateY(-20px) scale(0.8)';
                this.nextElementSibling.style.color = '#8e8e8e';
            });
            
            input.addEventListener('blur', function() {
                if (!this.value) {
                    this.nextElementSibling.style.transform = '';
                    this.nextElementSibling.style.color = '#8e8e8e';
                }
            });
        });
    </script>
</body>
</html>ew
