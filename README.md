#primer proyecto andres

import csv
import os

def menu_user():
    students = []
    
    while True:
        try:
            n = int(input("Enter the number of students: "))
            break
        except ValueError:
            print("Please enter a valid number ")

    while True:
        print("\nMenu: ")
        print(f"1. Enter information for {n} students")
        print("2. Show information of all students")
        print("3. View the top 3 students")
        print("4. View average grade for all students")
        print("5. Export all data to a CSV file")
        print("6. Import data from a previous exported CSV file")
        print("7. Exit program")

        option = input("Select an option from [1-7]: ")

        if option == '1':
            students = enter_students(n)
        elif option == '2':
            show_students(students)
        elif option == '3':
            view_top_3(students)
        elif option == '4':
            view_general_average(students)
        elif option == '5':
            export_csv(students)
        elif option == '6':
            students = import_csv()
        elif option == '7':
            print("Exit the program")
            break
        else:
            print("Invalid option, select an option from the menu [1-7]")

def validate_grade(grade):
    while True:
        try:
            value = float(grade)
            if 0 <= value <= 100:
                return value
            else:
                print("The grade must be between 0 and 100 ")
                grade = float(input("Enter the grade again: "))
        except ValueError:
            print("Invalid input, enter a grade between 0 and 100")
            grade = float(input("Enter the grade again 'number': "))

def enter_students(n):
    students = []
    for repetition in range(n):
        print(f"\nInformation for student {repetition+1}:")
        name = input("Full name: ")
        section = input("Section (e.g., 11b): ")
        spanish_grade = validate_grade(input("Spanish grade: "))
        english_grade = validate_grade(input("English grade: "))
        social_studies_grade = validate_grade(input("Social studies grade: "))
        science_grade = validate_grade(input("Science grade: "))
        
        student = {
            'name': name,
            'section': section,
            'grades': {
                'spanish': spanish_grade,
                'english': english_grade,
                'social_studies': social_studies_grade,
                'science': science_grade,
            }
        }
        students.append(student)
    return students

def show_students(students):
    print("\nInformation of students: ")
    for index, student in enumerate(students, start=1):
        print(f"\nStudent {index}:")
        print(f"Name: {student['name']}")
        print(f"Section: {student['section']}")
        print("Grades: ")
        for subject, grade in student['grades'].items():
            print(f"  {subject}: {grade}")

def view_top_3(students):
    if len(students) < 3:
        print("There are fewer than 3 students")
        return

    student_averages = []
    for student in students:
        grades = student['grades'].values()
        average = sum(grades) / len(grades)
        student_averages.append((student, average))

    for i in range(len(student_averages)):
        for j in range(i + 1, len(student_averages)):
            if student_averages[i][1] < student_averages[j][1]:
                student_averages[i], student_averages[j] = student_averages[j], student_averages[i]

    print("\nTop 3 students with highest averages:")
    for i in range(3):
        student, average = student_averages[i]
        print(f"{i+1}. {student['name']} - Average: {average:.2f}")

def view_general_average(students):
    total_average = 0
    for student in students:
        student_grades = student['grades'].values()
        student_average = sum(student_grades) / len(student_grades)
        total_average += student_average

    if len(students) > 0:
        general_average = total_average / len(students)
        print(f"\nThe general average of students is: {general_average:.2f}")
    else:
        print("No average")

def export_csv(students):
    file_path = r'C:\Users\andre\Desktop\lyfter andres\proyectos\students_data.csv'
    with open(file_path, mode='w', newline='') as file:
        writer = csv.writer(file)
        writer.writerow(['Name', 'Section', 'Spanish Grade', 'English Grade', 'Social Studies Grade', 'Science Grade'])
        for student in students:
            writer.writerow([
                student['name'],
                student['section'],
                student['grades']['spanish'],
                student['grades']['english'],
                student['grades']['social_studies'],
                student['grades']['science']
            ])
    print(f"Data exported to '{file_path}'")

def import_csv():
    file_path = input("Enter the CSV file path or press Enter to use the default path:  ")
    if not file_path:
        file_path = r'C:\Users\andre\Desktop\lyfter andres\proyectos\students_data.csv'

    if not os.path.exists(file_path):
        print(f"No previously exported file found: {file_path}")
        return []

    students = []
    with open(file_path, mode='r') as file:
        reader = csv.reader(file)
        next(reader)
        for row in reader:
            name, section, spanish_grade, english_grade, social_studies_grade, science_grade = row
            student = {
                'name': name,
                'section': section,
                'grades': {
                    'spanish': float(spanish_grade),
                    'english': float(english_grade),
                    'social_studies': float(social_studies_grade),
                    'science': float(science_grade)
                }
            }
            students.append(student)

    print(f"Data imported from '{file_path}'")
    return students


def main():
    menu_user()
    show_students()
    enter_students()
    validate_grade()
    view_top_3()
    view_general_average()
    export_csv()
    import_csv ()
if __name__ == "__main__":
    main()

