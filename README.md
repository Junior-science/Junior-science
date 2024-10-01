START

PROMPT USER

    "Select user type: (1) Student (2) Lecturer (3) Admin (4) Exit"
    INPUT userType

    IF userType == 1 THEN
        // Student login
        PRINT "Enter your name: "
        INPUT studentName
        IF studentName exists in students THEN
            CALL viewMarks(studentName)
        ELSE
            PRINT "Student not found."
        ENDIF
        CONTINUE LOOP

    ELSE IF userType == 2 THEN
        // Lecturer login
        PRINT "Enter your name: "
        INPUT lecturerName

        IF lecturerName exists in lecturers THEN
            PRINT "Enter password: "
            INPUT password

            IF password matches lecturers[lecturerName].password THEN
                LOOP
                    PRINT "Options: (1) View all marks (2) Modify mark (3) Add student (4) Logout"
                    INPUT lecturerOption

                    IF lecturerOption == 1 THEN
                        CALL viewAllMarks(lecturerName)
                    
                    ELSE IF lecturerOption == 2 THEN
                        PRINT "Enter student name: "
                        INPUT studentName
                        PRINT "Enter mark: "
                        INPUT mark
                        CALL modifyMark(lecturerName, studentName, mark)

                    ELSE IF lecturerOption == 3 THEN
                        PRINT "Enter student name: "
                        INPUT studentName
                        CALL addStudentToLecturer(lecturerName, studentName)

                    ELSE IF lecturerOption == 4 THEN
                        BREAK // Logout

                    ENDIF
                END LOOP
            ELSE
                PRINT "Incorrect password."
            ENDIF
        ELSE
            PRINT "Lecturer not found."
        ENDIF
        CONTINUE LOOP

    ELSE IF userType == 3 THEN
        // Admin login
        PRINT "Enter password: "
        INPUT adminPassword

        IF adminPassword matches admin.password THEN
            LOOP
                PRINT "Options: (1) Add Lecturer (2) View all marks (3) Add Student (4) Logout"
                INPUT adminOption

                IF adminOption == 1 THEN
                    PRINT "Enter lecturer name: "
                    INPUT lecturerName
                    PRINT "Enter lecturer password: "
                    INPUT lecturerPassword
                    PRINT "Enter subject for the lecturer: "
                    INPUT subject
                    CALL addLecturer(lecturerName, lecturerPassword, subject)

                ELSE IF adminOption == 2 THEN
                    CALL viewAllMarksForAllLecturers()

                ELSE IF adminOption == 3 THEN
                    PRINT "Enter student name: "
                    INPUT studentName
                    CALL addStudent(studentName)

                ELSE IF adminOption == 4 THEN
                    BREAK // Logout

                ENDIF
            END LOOP
        ELSE
            PRINT "Incorrect password."
        ENDIF
        CONTINUE LOOP

    ELSE IF userType == 4 THEN
        PRINT "Exiting..."
        BREAK
    ENDIF
END LOOP
