<!DOCTYPE html>
<html>
<head>
    <title>Attendance and Location</title>
</head>
<body>
    <h1>Login to Mark Attendance</h1>
    <div id="login-section">
        <label for="username">Name:</label>
        <input type="text" id="username" placeholder="Enter your name" required>
        <button onclick="markAttendance()">Login and Mark Attendance</button>
    </div>
    <p id="status"></p>

    <script>
        function markAttendance() {
            const username = document.getElementById('username').value;

            if (!username) {
                alert("Please enter your name.");
                return;
            }

            if (navigator.geolocation) {
                document.getElementById("status").innerText = "Fetching location...";
                navigator.geolocation.getCurrentPosition((position) => {
                    const latitude = position.coords.latitude;
                    const longitude = position.coords.longitude;

                    const attendanceData = {
                        name: username,
                        timestamp: new Date().toISOString(),
                        location: `https://www.google.com/maps?q=${latitude},${longitude}`
                    };

                    // Log attendance to console (replace this with a backend or database call)
                    console.log("Attendance Marked:", attendanceData);
                    document.getElementById("status").innerHTML = `
                        Attendance marked for ${attendanceData.name}!<br>
                        <a href="${attendanceData.location}" target="_blank">View Location on Map</a>
                    `;
                }, (error) => {
                    alert("Unable to fetch location. Please allow location access.");
                });
            } else {
                alert("Geolocation is not supported by your browser.");
            }
        }
    </script>
</body>
</html>
