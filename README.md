# day-15-task
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form to Table with DOM Manipulation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 0;
        }

        form {
            margin-bottom: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            background-color: #f9f9f9;
        }

        form div {
            margin-bottom: 10px;
        }

        form label {
            display: inline-block;
            width: 100px;
        }

        form input, form select {
            width: 200px;
            padding: 5px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        table, th, td {
            border: 1px solid #ccc;
        }

        th, td {
            padding: 10px;
            text-align: left;
        }

        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>
    <h1>Form Submission and Table Update</h1>
    <form id="userForm">
        <div>
            <label for="firstName">First Name:</label>
            <input type="text" id="firstName" required>
        </div>
        <div>
            <label for="lastName">Last Name:</label>
            <input type="text" id="lastName" required>
        </div>
        <div>
            <label for="email">Email:</label>
            <input type="email" id="email" required>
        </div>
        <div>
            <label for="address">Address:</label>
            <input type="text" id="address" required>
        </div>
        <div>
            <label for="pincode">Pincode:</label>
            <input type="text" id="pincode" required>
        </div>
        <div>
            <label for="gender">Gender:</label>
            <select id="gender" required>
                <option value="">Select</option>
                <option value="Male">Male</option>
                <option value="Female">Female</option>
                <option value="Other">Other</option>
            </select>
        </div>
        <div>
            <label for="food">Choice of Food:</label>
            <select id="food" required>
                <option value="">Select</option>
                <option value="Vegetarian">Vegetarian</option>
                <option value="Non-Vegetarian">Non-Vegetarian</option>
                <option value="Vegan">Vegan</option>
            </select>
        </div>
        <div>
            <label for="state">State:</label>
            <input type="text" id="state" required>
        </div>
        <div>
            <label for="country">Country:</label>
            <input type="text" id="country" required>
        </div>
        <div>
            <button type="submit">Submit</button>
        </div>
    </form>

    <table id="userTable">
        <thead>
            <tr>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Email</th>
                <th>Address</th>
                <th>Pincode</th>
                <th>Gender</th>
                <th>Food</th>
                <th>State</th>
                <th>Country</th>
            </tr>
        </thead>
        <tbody>
        </tbody>
    </table>

    <script>
        document.getElementById('userForm').addEventListener('submit', function(event) {
            event.preventDefault();

            // Get form values
            const firstName = document.getElementById('firstName').value;
            const lastName = document.getElementById('lastName').value;
            const email = document.getElementById('email').value;
            const address = document.getElementById('address').value;
            const pincode = document.getElementById('pincode').value;
            const gender = document.getElementById('gender').value;
            const food = document.getElementById('food').value;
            const state = document.getElementById('state').value;
            const country = document.getElementById('country').value;

            // Create a new table row
            const row = document.createElement('tr');

            // Append cells to the row
            row.innerHTML = `
                <td>${firstName}</td>
                <td>${lastName}</td>
                <td>${email}</td>
                <td>${address}</td>
                <td>${pincode}</td>
                <td>${gender}</td>
                <td>${food}</td>
                <td>${state}</td>
                <td>${country}</td>
            `;

            // Append the row to the table body
            document.querySelector('#userTable tbody').appendChild(row);

            // Clear the form fields
            document.getElementById('userForm').reset();
        });
    </script>

    <!-- Test Suite -->
    <script>
        (function() {
            const testFormSubmission = () => {
                const testForm = document.getElementById('userForm');
                const testTable = document.getElementById('userTable');

                // Set test values
                document.getElementById('firstName').value = 'John';
                document.getElementById('lastName').value = 'Doe';
                document.getElementById('email').value = 'john.doe@example.com';
                document.getElementById('address').value = '123 Main St';
                document.getElementById('pincode').value = '123456';
                document.getElementById('gender').value = 'Male';
                document.getElementById('food').value = 'Vegan';
                document.getElementById('state').value = 'California';
                document.getElementById('country').value = 'USA';

                // Simulate form submission
                testForm.querySelector('button[type="submit"]').click();

                // Check if the table has the new row
                const lastRow = testTable.querySelector('tbody tr:last-child');
                if (!lastRow) {
                    console.error('Test Failed: No row added to the table.');
                    return;
                }

                const cells = lastRow.querySelectorAll('td');
                if (cells.length !== 9 ||
                    cells[0].textContent !== 'John' ||
                    cells[1].textContent !== 'Doe' ||
                    cells[2].textContent !== 'john.doe@example.com' ||
                    cells[3].textContent !== '123 Main St' ||
                    cells[4].textContent !== '123456' ||
                    cells[5].textContent !== 'Male' ||
                    cells[6].textContent !== 'Vegan' ||
                    cells[7].textContent !== 'California' ||
                    cells[8].textContent !== 'USA') {
                    console.error('Test Failed: The row data is incorrect.');
                    return;
                }

                console.log('Test Passed: The form submission and table update worked as expected.');
            };

            window.addEventListener('load', () => {
                testFormSubmission();
            });
        })();
    </script>
</body>
</html>
