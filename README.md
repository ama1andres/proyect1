#primer proyecto andres
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
            print
            #investigar como
        elif option == '7':
            print("Exit the program")
            break
        else:
            print("invalid option, select an option from the menu [1-7]")


def validate_grade(grade):
    while True:
        try:
            value = float(grade)
            if 0 <= value <= 100:
                return value
            
            else:
                print("The grade must be between 0 and 100 ")
                grade = int(input("Enter the grade again: "))
        except ValueError:
            print("Invalid input enter a grade between 0 and 100")
            grade = int(input("Enter the grade again 'number': "))

def enter_students(n):
    students = []
    for repetition in range(n):
        print(f"\n information for student {repetition+1}:")
        name = input("Full name: ")
        section = input("Section ej 11b: ")
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
    print("\nInformation all students: ")

    for index, student in enumerate(students, start=1):

        print(f"\nStudent {index}:")
        print(f"Name: {student['name']}")
        print(f"Section: {student['section']}")
        print("Grades:")
        
        for subject, grade in student['grades'].items():

            print(f"  {subject}: {grade}")


def view_top_3 (students):
    print()


def  view_general_average():
    print()


def  export_csv ():
    print()


def  import_csv ():
    print()


def main():
    menu_user()
    show_students()
    enter_students()
    validate_grade()
    view_top_3()
    view_general_average()
    view_top_3()
    export_csv()
    import_csv ()
if __name__ == "__main__":
    main()
