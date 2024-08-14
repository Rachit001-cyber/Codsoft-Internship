//Task 5
import java.util.*;

public class CourseRegistrationSystem {
    // Database for courses and students
    private static final Map<String, Course> courses = new HashMap<>();
    private static final Map<String, Student> students = new HashMap<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        initializeCourses(); // Sample data
        initializeStudents(); // Sample data

        while (true) {
            System.out.println("\n--- Course Registration System ---");
            System.out.println("1. Display Available Courses");
            System.out.println("2. Register for a Course");
            System.out.println("3. Drop a Course");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    displayCourses();
                    break;
                case 2:
                    registerForCourse(scanner);
                    break;
                case 3:
                    dropCourse(scanner);
                    break;
                case 4:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }

    private static void initializeCourses() {
        courses.put("CS101", new Course("CS101", "Introduction to Computer Science", "Basics of computer science", 30, "MWF 10:00-11:00"));
        courses.put("MATH202", new Course("MATH202", "Calculus II", "Advanced calculus topics", 25, "TTh 13:00-14:30"));
        courses.put("HIST303", new Course("HIST303", "World History", "History of the world", 20, "MW 15:00-16:30"));
    }

    private static void initializeStudents() {
        students.put("S001", new Student("S001", "Alice Smith"));
        students.put("S002", new Student("S002", "Bob Johnson"));
        students.put("S003", new Student("S003", "Carol White"));
    }

    private static void displayCourses() {
        System.out.println("\nAvailable Courses:");
        for (Course course : courses.values()) {
            System.out.println(course);
        }
    }

    private static void registerForCourse(Scanner scanner) {
        System.out.print("Enter student ID: ");
        String studentId = scanner.nextLine();
        Student student = students.get(studentId);

        if (student == null) {
            System.out.println("Student not found.");
            return;
        }

        System.out.print("Enter course code to register for: ");
        String courseCode = scanner.nextLine();
        Course course = courses.get(courseCode);

        if (course == null) {
            System.out.println("Course not found.");
            return;
        }

        if (course.getCapacity() <= 0) {
            System.out.println("Course is full.");
            return;
        }

        student.registerCourse(course);
        course.registerStudent();
        System.out.println("Registered successfully.");
    }

    private static void dropCourse(Scanner scanner) {
        System.out.print("Enter student ID: ");
        String studentId = scanner.nextLine();
        Student student = students.get(studentId);

        if (student == null) {
            System.out.println("Student not found.");
            return;
        }

        System.out.print("Enter course code to drop: ");
        String courseCode = scanner.nextLine();
        Course course = courses.get(courseCode);

        if (course == null) {
            System.out.println("Course not found.");
            return;
        }

        if (!student.dropCourse(course)) {
            System.out.println("Not registered for this course.");
            return;
        }

        course.deregisterStudent();
        System.out.println("Dropped successfully.");
    }
}

class Course {
    private final String code;
    private final String title;
    private final String description;
    private int capacity;
    private final String schedule;
    private final Set<Student> registeredStudents = new HashSet<>();

    public Course(String code, String title, String description, int capacity, String schedule) {
        this.code = code;
        this.title = title;
        this.description = description;
        this.capacity = capacity;
        this.schedule = schedule;
    }

    public String getCode() {
        return code;
    }

    public int getCapacity() {
        return capacity;
    }

    public void registerStudent() {
        if (capacity > 0) {
            capacity--;
        }
    }

    public void deregisterStudent() {
        capacity++;
    }

    @Override
    public String toString() {
        return String.format("Course Code: %s\nTitle: %s\nDescription: %s\nAvailable Slots: %d\nSchedule: %s\n",
                code, title, description, capacity, schedule);
    }
}

class Student {
    private final String id;
    private final String name;
    private final Set<Course> registeredCourses = new HashSet<>();

    public Student(String id, String name) {
        this.id = id;
        this.name = name;
    }

    public void registerCourse(Course course) {
        registeredCourses.add(course);
    }

    public boolean dropCourse(Course course) {
        if (registeredCourses.remove(course)) {
            return true;
        }
        return false;

    }
}

