# Age-Calculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Age Calculator</title>
    <style>
        h1{
            color:#cd1010; 
            font-weight: 900;
            font-family: 'Times New Roman', Times, serif;
        }
        p{
            color:#cd1010; 
            font-family: 'Times New Roman', Times, serif;
            font-size: 20px;
        }
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(-45deg, #000000 0%, #cd1010 100%);
            color: rgb(170, 18, 18);
            overflow: hidden;
            animation: backgroundShift 6s infinite;
        }

        @keyframes backgroundShift {
            0% {
                background-position: 0% 50%;
            }
            50% {
                background-position: 100% 50%;
            }
            100% {
                background-position: 0% 50%;
            }
        }

        h1 {
            margin-bottom: 20px;
            font-size: 36px;
            text-align: center;
            color: rgb(177, 6, 6);
            animation: fadeIn 1.5s ease-out;
        }

        @keyframes fadeIn {
            0% {
                opacity: 0;
            }
            100% {
                opacity: 1;
            }
        }

        .calculator-container {
            background: rgb(0, 0, 0);
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.918);
            animation: popUp 1.5s ease-out;
            text-align: center;
            width: 350px;
        }

        @keyframes popUp {
            0% {
                transform: scale(0.9);
                opacity: 0;
            }
            100% {
                transform: scale(1);
                opacity: 1;
            }
        }

        form {
            display: flex;
            flex-direction: column;
            gap: 20px;
            align-items: center; /* Align inputs centrally */
            opacity: 0;
            animation: formFadeIn 2s forwards;
        }

        @keyframes formFadeIn {
            0% {
                opacity: 0;
                transform: translateY(50px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }

        label {
            font-weight: bold;
            display: block;
            margin-bottom: 5px;
        }

        /* New Input Theme */
        .input, .select {
            background-color: #fefffe;
            border: none;
            width: 100%;
            max-width: 300px;
            height: 56px;
            border-radius: 10px;
            color: rgb(15, 14, 14);
            padding-inline: 20px;
            font-size: 18px;
            position: relative;
            margin-bottom: 15px;
            animation: inputAnim 0.5s ease-out forwards;
        }

        .input::placeholder {
            color: #c0b9c0;
        }

        .input:focus, .select:focus {
            outline: none;
        }

        @keyframes inputAnim {
            0% {
                opacity: 0;
                transform: translateY(30px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Button Styling */
        .button {
            position: relative;
            width: 120px;
            height: 40px;
            background-color: #ffffff;
            display: flex;
            align-items: center;
            justify-content: center;
            color: rgb(10, 10, 10);
            flex-direction: column;
            border: none;
            padding: 12px;
            gap: 12px;
            border-radius: 8px;
            cursor: pointer;
            margin: 0 auto; /* Center the button */
            animation: buttonAnim 0.5s ease-out forwards;
        }

        @keyframes buttonAnim {
            0% {
                opacity: 0;
                transform: translateY(20px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .button::before {
            content: '';
            position: absolute;
            inset: 0;
            left: -4px;
            top: -1px;
            margin: auto;
            width: 128px;
            height: 48px;
            border-radius: 10px;
            background: linear-gradient(-45deg, #e81cff 0%, #40c9ff 100%);
            z-index: -10;
            pointer-events: none;
            transition: all 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .button::after {
            content: "";
            z-index: -1;
            position: absolute;
            inset: 0;
            background: linear-gradient(-45deg, #fc00ff 0%, #00dbde 100%);
            transform: translate3d(0, 0, 0) scale(0.95);
            filter: blur(20px);
        }

        .button:hover::after {
            filter: blur(30px);
        }

        .button:hover::before {
            transform: rotate(-180deg);
        }

        .button:active::before {
            scale: 0.7;
        }

        .result {
            margin-top: 15px;
            font-size: 18px;
            font-weight: bold;
            color: #ff7eb3;
            animation: slideUp 1s ease-out forwards;
        }

        @keyframes slideUp {
            0% {
                opacity: 0;
                transform: translateY(20px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</head>
<body>
    <div class="calculator-container">
        <h1>Age Calculator</h1>
        <form id="ageCalculator">
            <label for="day">Day:</label>
            <input type="number" id="day" class="input" min="1" max="31" placeholder="Enter day" required>
            
            <label for="month">Month:</label>
            <select id="month" class="select" required>
                <option value="" disabled selected>Select Month</option>
                <option value="january">January</option>
                <option value="february">February</option>
                <option value="march">March</option>
                <option value="april">April</option>
                <option value="may">May</option>
                <option value="june">June</option>
                <option value="july">July</option>
                <option value="august">August</option>
                <option value="september">September</option>
                <option value="october">October</option>
                <option value="november">November</option>
                <option value="december">December</option>
            </select>
            
            <label for="year">Year:</label>
            <input type="number" id="year" class="input" min="1900" placeholder="Enter year" required>
            
            <button type="button" class="button" onclick="calculateAge()">Calculate Age</button>
        </form>
        <div class="result" id="result"></div>
    </div>

    <script>
        function calculateAge() {
            const day = document.getElementById('day').value;
            const month = document.getElementById('month').value.toLowerCase();
            const year = document.getElementById('year').value;

            if (!day || !month || !year) {
                document.getElementById('result').innerText = "Please fill in all fields.";
                return;
            }

            const monthMap = {
                january: 0, february: 1, march: 2, april: 3, may: 4, june: 5,
                july: 6, august: 7, september: 8, october: 9, november: 10, december: 11
            };

            if (!(month in monthMap)) {
                document.getElementById('result').innerText = "Invalid month. Please select a valid month.";
                return;
            }

            const birthDate = new Date(year, monthMap[month], day);
            const today = new Date();

            if (birthDate > today) {
                document.getElementById('result').innerText = "Future dates are invalid!";
                return;
            }

            let age = today.getFullYear() - birthDate.getFullYear();
            const monthDiff = today.getMonth() - birthDate.getMonth();
            const dayDiff = today.getDate() - birthDate.getDate();

            if (monthDiff < 0 || (monthDiff === 0 && dayDiff < 0)) {
                age--;
            }

            document.getElementById('result').innerText = `You are ${age} years old.`;
        }
    </script>
</body>
</html>
