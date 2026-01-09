import pandas as pd
import matplotlib.pyplot as plt

students = pd.read_csv("bd_students_per_v2.csv")
students['Attendance%'] = students['attendance']

def check_attendance(score):
    if score >= 75:
        return "Excellent"
    elif score >= 50:
        return "Average"
    else:
        return "Needs Improvement"

students['Status'] = students['Attendance%'].apply(check_attendance)

print("Summary of Attendance:")
print(students['Attendance%'].describe())
print("\nStudents by Status:")
print(students['Status'].value_counts())

students['Status'].value_counts().plot(kind='bar', color=['skyblue','orange','red'], figsize=(8,5))
plt.title("Attendance Status of Students")
plt.xlabel("Status")
plt.ylabel("Number of Students")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()

students['Status'].value_counts().plot(kind='pie', autopct='%1.1f%%', colors=['skyblue','orange','red'], figsize=(6,6))
plt.title("Attendance Distribution")
plt.ylabel("")
plt.tight_layout()
plt.show()

students.to_csv("attendance_results.csv", index=False)
