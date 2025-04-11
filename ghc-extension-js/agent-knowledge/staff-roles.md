Below is a list of common roles and tasks they might want help with.
If a user specifies their role, you can use this information to provide more targeted suggestions or offer ways to help them.

## School Administration

- Budget management and resource allocation
- Staff recruitment, management, and development
- School improvement plans, vision setting, and culture building
- Community relations

## Instructional Staff

- Curriculum planning and lesson design
- Grading and performance tracking
- Course customization and differentiation for students
- Parent communication and student support
- Classroom management and behavior systems

```javascript
import express from "express";
import bodyParser from "body-parser";

const app = express();
app.use(bodyParser.json());

// Mock database
const students = [];

// API to add a student
app.post("/students", (req, res) => {
  const student = req.body;
  students.push(student);
  res.status(201).send({ message: "Student added", student });
});

// API to get all students
app.get("/students", (req, res) => {
  res.send(students);
});

// API to get student grades
app.get("/student-grades", (req, res) => {
  // Example data structure for grades
  const grades = [
    { name: "Alice", grades: [85, 90, 88, 92] },
    { name: "Bob", grades: [78, 82, 80, 85] },
  ];
  res.send(grades);
});

// Start the server
const port = 3000;
app.listen(port, () => {
  console.log(`Student tracker running at http://localhost:${port}`);
});
```

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Student Grades Visualization</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
  <h1>Student Grades Over Time</h1>
  <canvas id="gradesChart" width="400" height="200"></canvas>

  <script>
    async function loadGrades() {
      const res = await fetch("/student-grades");
      const data = await res.json();

      const labels = ["Q1", "Q2", "Q3", "Q4"]; // Example time periods
      const datasets = data.map((student) => ({
        label: student.name,
        data: student.grades,
        borderColor: getRandomColor(),
        fill: false,
      }));

      const ctx = document.getElementById("gradesChart").getContext("2d");
      new Chart(ctx, {
        type: "line",
        data: {
          labels,
          datasets,
        },
        options: {
          responsive: true,
          plugins: {
            legend: {
              position: "top",
            },
          },
        },
      });
    }

    function getRandomColor() {
      return `rgba(${Math.floor(Math.random() * 255)}, ${Math.floor(
        Math.random() * 255
      )}, ${Math.floor(Math.random() * 255)}, 1)`;
    }

    loadGrades();
  </script>
</body>
</html>
