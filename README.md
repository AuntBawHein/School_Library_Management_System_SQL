# School_Library_Management_System_SQL

-- The scope of this project is to design a School Library Management System Project. 
-- Problem statement / idea 
-- 1. We have to think how we're going to create lots of objects first, before adding more attributes. 
-- 2. Think and create about entities or attributes inside lots of objects. 
-- 3. Design and create ER diagram. 
-- 4. Finally, run each table to make sure that ER diagrams are in one place. 

-- Below are the processes and questions that I'm going to create step by step based on this project here. 








-- Step 1: I'm going to create 10 objects for School Library Management Sytem. 
-- Here, these are our objects. 
-- 1. Author 
-- 2. Genre 
-- 3. Publisher 
-- 4. Class 
-- 5. Section 
-- 6. Student 
-- 7. Teacher 
-- 8. Books 
-- 9. Library Attendance 
-- 10. Library Management 






-- Step 2: Let's create our table here one by one. 
-- Authors Table
CREATE TABLE Authors (
    Au_id INT PRIMARY KEY,
    Au_name VARCHAR(100),
    Au_age INT,
    Au_email VARCHAR(100),
    Au_country VARCHAR(50)
);
-- Genres Table
CREATE TABLE Genres (
    Genre_id INT PRIMARY KEY,
    Genre_name VARCHAR(50),
    Genre_description VARCHAR(255)
);



-- Publishers Table
CREATE TABLE Publishers (
    Pub_id INT PRIMARY KEY,
    Pub_name VARCHAR(100),
    Pub_address VARCHAR(255),
    Pub_contact_person VARCHAR(100)
);

-- Classes Table
CREATE TABLE Classes (
    Cl_id INT PRIMARY KEY,
    Cl_name VARCHAR(20),
    Cl_teacher_name VARCHAR(100),
    Cl_room_number VARCHAR(10)
);



-- Sections Table
CREATE TABLE Sections (
    Sect_id INT PRIMARY KEY,
    Sect_name VARCHAR(20),
    Cl_id INT,
    Sect_teacher VARCHAR(100),
    FOREIGN KEY (Cl_id) REFERENCES Classes(Cl_id)
);










- Students Table
CREATE TABLE Students (
    St_id INT PRIMARY KEY,
    St_firstname VARCHAR(50),
    St_lastname VARCHAR(50),
    St_age INT,
    St_gender VARCHAR(100),
    St_nationality VARCHAR(100),
    St_address VARCHAR(100),
    St_email VARCHAR(100),
    St_ph_number VARCHAR(100),
    St_grade_id INT,
    Sect_id INT,
    FOREIGN KEY (St_grade_id) REFERENCES Classes(Cl_id),
    FOREIGN KEY (Sect_id) REFERENCES Sections(Sect_id)
);


-- Teachers Table
CREATE TABLE Teachers (
    Tea_id INT PRIMARY KEY,
    Tea_firstname VARCHAR(50),
    Tea_lastname VARCHAR(50),
    Tea_age INT,
    Tea_gender VARCHAR(100),
    Tea_nationality VARCHAR(100),
    Tec_address VARCHAR(100),
    Tea_ph_number VARCHAR(100),
    Tea_email VARCHAR(100),
    St_id INT,
    Sect_id INT,
    FOREIGN KEY (St_id) REFERENCES Students(St_id),
    FOREIGN KEY (Sect_id) REFERENCES Sections(Sect_id)
);


-- Books Table
CREATE TABLE Books (
    Bk_id INT PRIMARY KEY,
    Bk_title VARCHAR(255),
    Bk_ISBN_id VARCHAR(100),
    Bk_quantity_available INT,
    Bk_published_year INT,
    Bk_description VARCHAR(255),
    Au_id INT,
    Genre_id INT,
    Pub_id INT,
    FOREIGN KEY (Au_id) REFERENCES Authors(Au_id),
    FOREIGN KEY (Genre_id) REFERENCES Genres(Genre_id),
    FOREIGN KEY (Pub_id) REFERENCES Publishers(Pub_id)
);



-- Library_Attendance Table
CREATE TABLE Library_Attendance (
    Lib_attend_id INT PRIMARY KEY,
    Lib_attend_date DATE,
    Lib_attend_St_firstname VARCHAR(100),
    Lib_attend_St_lastname VARCHAR(100),
    Lib_attend_St_gender VARCHAR(100),
    Lib_attend_St_borrow_date DATE,
    Lib_attend_St_return_date DATE,
    Lib_attend_St_borrow_books_num INT,
    St_id INT,
    FOREIGN KEY (St_id) REFERENCES Students(St_id)
);





-- Library_Management Table
CREATE TABLE Library_Management (
    Lib_management_id INT PRIMARY KEY,
    Lib_management_name VARCHAR(100),
    Lib_management_description VARCHAR(100),
    Au_id INT,
    Genre_id INT,
    FOREIGN KEY (Au_id) REFERENCES Authors(Au_id),
    FOREIGN KEY (Genre_id) REFERENCES Genres(Genre_id)
);








-- Inserting data into Authors Table
INSERT INTO Authors (Au_id, Au_name, Au_age, Au_email, Au_country) VALUES
(4, 'Alicia Chang', 45, 'alicia_chang@gmail.com', 'USA'),
(5, 'Ravi Kapoor', 55, 'ravi_kapoor@gmail.com', 'India'),
(6, 'Sophie Dubois', 42, 'sophie_dubois@gmail.com', 'France'),
(7, 'Hiroshi Tanaka', 48, 'hiroshi_tanaka@gmail.com', 'Japan'),
(8, 'Isabella Rossi', 40, 'isabella_rossi@gmail.com', 'Italy'),
(9, 'Carlos Rodriguez', 52, 'carlos_rodriguez@gmail.com', 'Spain'),
(10, 'Yuki Kimura', 36, 'yuki_kimura@gmail.com', 'Japan'),
(11, 'Olga Petrov', 47, 'olga_petrov@gmail.com', 'Russia'),
(12, 'Feng Chen', 44, 'feng_chen@gmail.com', 'China'),
(13, 'Diego Hernandez', 39, 'diego_hernandez@gmail.com', 'Mexico');

-- Showing all the ouputs or informations of Authors table.
SELECT * FROM Authors;



-- Newid () function used to generate any random information.
SELECT * FROM Authors 
ORDER BY NEWID();

-- Inserting data into Genres Table
INSERT INTO Genres (Genre_id, Genre_name, Genre_description) VALUES
(14, 'Fantasy', 'Books set in imaginary worlds with magical elements.'),
(16, 'Science Fiction', 'Books exploring futuristic concepts and technology.'),
(19, 'Romance', 'Books focusing on romantic relationships and love stories.'),
(17, 'Biography', 'Books narrating the life stories of real people.'),
(18, 'Self-Help', 'Books providing guidance and advice for personal development.'),
(15, 'Poetry', 'Books featuring expressive and artistic use of language.'),
(20, 'Thriller', 'Books designed to keep readers on the edge of their seats.'),
(21, 'Cooking', 'Books containing recipes and culinary techniques.'),
(22, 'Travel', 'Books exploring different places and cultures.'),
(23, 'Drama', 'Books with intense and emotional storytelling.');


-- Showing all the outputs or informations in Genres table.
SELECT * FROM Genres;

-- Newid function() used to generate any random information.
SELECT * FROM Genres 
ORDER BY NEWID();












-- Inserting data into Publishers Table
INSERT INTO Publishers (Pub_id, Pub_name, Pub_address, Pub_contact_person) VALUES
(24, 'Global Books Ltd.', 'New York', 'Emily Johnson'),
(27, 'Sunrise Publishing House', 'London', 'David Anderson'),
(25, 'Golden Pages', 'Paris', 'Sophie Martin'),
(26, 'Epic Publications', 'Berlin', 'Maximilian Müller'),
(28, 'Rainbow Press', 'Tokyo', 'Yuki Tanaka'),
(29, 'Starlight Books', 'Sydney', 'Olivia Lee'),
(30, 'Pacific Publishers', 'Vancouver', 'Ethan Campbell'),
(31, 'Mountain View Press', 'Cape Town', 'Liam Ngubane'),
(32, 'Aurora Publications', 'Mumbai', 'Neha Kapoor'),
(33, 'Penguin Books', 'Toronto', 'Michael Johnson');

-- Showing all the outputs or informations of Publishers table.
SELECT * FROM Publishers;



-- We use Newid () function to generate any random information.
SELECT * FROM Publishers 
ORDER BY NEWID();

-- Inserting data into Classes Table
INSERT INTO Classes (Cl_id, Cl_name, Cl_teacher_name, Cl_room_number) VALUES
(34, 'Class D', 'Mrs. Johnson', '404'),
(39, 'Class E', 'Mr. Patel', '505'),
(38, 'Class F', 'Ms. Garcia', '606'),
(35, 'Class G', 'Mr. Kim', '707'),
(37, 'Class H', 'Mrs. Smith', '808'),
(36, 'Class I', 'Mr. Tanaka', '909'),
(40, 'Class J', 'Ms. Martinez', '1010'),
(41, 'Class K', 'Mr. Chen', '1111'),
(42, 'Class L', 'Mrs. Nguyen', '1212'),
(43, 'Class M', 'Mr. Hernandez', '1313');


-- Showing all outputs or informations of Classes table.
SELECT * FROM Classes;

-- We use Newid() function to generate any random information.
SELECT * FROM Classes 
ORDER BY NEWID();












-- Inserting more data into Sections Table
INSERT INTO Sections (Sect_id, Sect_name, Cl_id, Sect_teacher) VALUES
(4, 'Section 4', 36, 'Mrs. Johnson'),
(5, 'Section 5', 39, 'Mr. Patel'),
(6, 'Section 6', 34, 'Ms. Garcia'),
(7, 'Section 7', 37, 'Mr. Kim'),
(8, 'Section 8', 38, 'Mrs. Smith'),
(9, 'Section 9', 35, 'Mr. Tanaka'),
(10, 'Section 10', 43, 'Ms. Martinez'),
(11, 'Section 11', 41, 'Mr. Chen'),
(12, 'Section 12', 42, 'Mrs. Nguyen'),
(13, 'Section 13', 40, 'Mr. Hernandez');

-- Showing all ouputs or informations of Sections table.
SELECT * FROM Sections 



-- Newdi() function used to generate any random information.
SELECT * FROM Sections 
ORDER BY NEWID();

-- Inserting more data into Students Table
INSERT INTO Students (St_id, St_firstname, St_lastname, St_age, St_gender, St_nationality, St_address, St_email, St_ph_number,Sect_id) 
VALUES
(32214, 'Oliver', 'Queen', 17, 'Male', 'USA', 'Starling City', 'oliver_queen@gmail.com', '086-334-9987',10),
(32215, 'Felicity', 'Smoak', 16, 'Female', 'USA', 'Central City', 'felicity_smoak@gmail.com', '088-456-1234', 13),
(32216, 'Barry', 'Allen', 15, 'Male', 'USA', 'Keystone City', 'barry_allen@gmail.com', '081-567-7890', 6),
(32217, 'Diana', 'Prince', 18, 'Female', 'Themyscira', 'Themyscira Island', 'diana_prince@gmail.com', '089-987-6543', 7),
(32218, 'Clark', 'Kent', 17, 'Male', 'USA', 'Smallville', 'clark_ke;nt@gmail.com', '084-123-5678', 8),
(32219, 'Bruce', 'Wayne', 18, 'Male', 'USA', 'Gotham City', 'bruce_wayne@gmail.com', '080-987-6542', 9),
(32220, 'Selina', 'Kyle', 16, 'Female', 'USA', 'Gotham City', 'selina_kyle@gmail.com', '082-654-7890', 11),
(32221, 'Jason', 'Todd', 17, 'Male', 'USA', 'Gotham City', 'jason_todd@gmail.com', '087-345-6789', 4),
(32222, 'Barbara', 'Gordon', 16, 'Female', 'USA', 'Gotham City', 'barbara_gordon@gmail.com', '085-876-5432', 5),
(32223, 'Dick', 'Grayson', 18, 'Male', 'USA', 'Gotham City', 'dick_grayson@gmail.com', '086-789-0123', 12);

-- Showing all outputs or informations of this table.
SELECT * FROM Students;


-- Newid() function is used to generate any random information.
SELECT * FROM Students 
ORDER BY NEWID();



-- Inserting data into Teachers Table
INSERT INTO Teachers (Tea_id, Tea_firstname, Tea_lastname, Tea_age, Tea_gender, Tea_nationality, Tec_address, Tea_ph_number, 
Tea_email, St_id, Sect_id) VALUES
(4, 'Ms. Emily', 'Smith', 28, 'Female', 'USA', 'Downtown', '086-123-4567', 'emily.smith@gmail.com', 32214, 4),
(5, 'Mr. Christopher', 'Williams', 40, 'Male', 'Canada', 'Uptown', '084-567-8901', 'christopher.williams@gmail.com', 32215, 5),
(6, 'Mrs. Aisha', 'Ahmed', 45, 'Female', 'Pakistan', 'Suburbia', '081-234-5678', 'aisha.ahmed@gmail.com', 32216, 6),
(7, 'Mr. Carlos', 'Rodriguez', 37, 'Male', 'Spain', 'City Center', '087-890-1234', 'carlos.rodriguez@gmail.com', 32217, 7),
(8, 'Dr. Mei', 'Wong', 55, 'Female', 'China', 'Chinatown', '083-456-7890', 'mei.wong@gmail.com', 32218, 8),
(9, 'Prof. Luca', 'Ricci', 48, 'Male', 'Italy', 'Little Italy', '080-123-4567', 'luca.ricci@gmail.com', 32219, 9),
(10, 'Mrs. Sofia', 'Garcia', 41, 'Female', 'Mexico', 'Downtown', '085-678-9012', 'sofia.garcia@gmail.com', 32220, 10),
(11, 'Mr. Abdul', 'Khan', 32, 'Male', 'India', 'Suburbia', '082-345-6789', 'abdul.khan@gmail.com', 32221, 11),
(12, 'Dr. Maria', 'Lopez', 50, 'Female', 'Argentina', 'City Center', '088-901-2345', 'maria.lopez@gmail.com', 32222, 12),
(13, 'Prof. Hiroshi', 'Tanaka', 55, 'Male', 'Japan', 'Tokyo District', '086-567-8901', 'hiroshi.tanaka@gmail.com', 32223, 13);

-- Showing all ouputs and information of this table.
SELECT * FROM Teachers;

-- Newid() function used to generate any random information.
SELECT * FROM Teachers 
ORDER BY NEWID();








-- Inserting data into Books Table
INSERT INTO Books (Bk_id, Bk_title, Bk_ISBN_id, Bk_quantity_available, Bk_published_year, Bk_description, Au_id, Genre_id, Pub_id) 
VALUES
(4, 'Data Structures and Algorithms', '978-0-12-345678-9', 12, 2008, 'A comprehensive guide to data structures and algorithms in computer science.', 4, 14, 24),
(5, 'The Art of Mystery Writing', '978-1-23-456789-0', 20, 2015, 'Unravel the secrets of crafting gripping mystery novels.', 5, 15, 25),
(6, 'Ancient Civilizations: A Historical Overview', '978-2-34-567890-1', 5, 1990, 'Explore the rise and fall of ancient civilizations from around the world.', 6, 16, 26),
(7, 'Artificial Intelligence: Concepts and Applications', '978-3-45-678901-2', 17, 2027, 'An in-depth exploration of AI concepts and their real-world applications.', 7, 17, 27),  -- Corrected Genre_id
(8, 'Modern Poetry Anthology', '978-4-56-789012-3', 15, 2019, 'A collection of contemporary poetry from various renowned poets.', 8, 15, 28),  -- Corrected Genre_id
(9, 'Financial Markets and Investment Strategies', '978-5-67-890123-4', 7, 2017, 'A guide to understanding financial markets and optimizing investment strategies.', 9, 19, 29),
(10, 'Space Exploration: Past, Present, and Future', '978-6-78-901234-5', 25, 2005, 'Journey through the history and future possibilities of space exploration.', 10, 20, 30),
(11, 'The Psychology of Human Behavior', '978-7-89-012345-6', 10, 2014, 'An insightful exploration into the complexities of human psychology.', 11, 21, 31),
(12, 'Environmental Science: A Global Perspective', '978-8-90-123456-7', 14, 2016, 'Examine environmental issues from a global standpoint with a focus on sustainability.', 12, 22, 32),
(13, 'Digital Marketing Strategies for Success', '978-9-01-234567-8', 22, 2020, 'A comprehensive guide to leveraging digital marketing for business success.', 13, 23, 33);


-- Showing all outputs or informations of this table. 
SELECT * FROM Books;

-- Newid() function used to generate any random information 
SELECT * FROM Books 
ORDER BY NEWID();

-- Inserting dat into Library Attendance table.
INSERT INTO Library_Attendance (Lib_attend_id, Lib_attend_date, Lib_attend_St_firstname, Lib_attend_St_lastname, Lib_attend_St_gender, 
Lib_attend_St_borrow_date, Lib_attend_St_return_date, Lib_attend_St_borrow_books_num, St_id) VALUES
(1, '2024-01-17', 'Gwen', 'Stacy', 'Female', '2024-01-15', '2024-01-20', 2, 32214),
(2, '2024-01-17', 'Donald', 'Trump', 'Male', '2024-01-14', '2024-01-19', 1, 32215),
(3, '2024-01-18', 'Will', 'Smith', 'Male', '2024-01-16', '2024-01-21', 3, 32216),
(4, '2024-01-18', 'Emma', 'Stone', 'Female', '2024-01-15', '2024-01-20', 2, 32217),
(5, '2024-01-19', 'John', 'Doe', 'Male', '2024-01-17', '2024-01-22', 1, 32218),
(6, '2024-01-19', 'Ava', 'Johnson', 'Female', '2024-01-16', '2024-01-21', 3, 32219),
(7, '2024-01-20', 'Michael', 'Jordan', 'Male', '2024-01-18', '2024-01-23', 2, 32220),
(8, '2024-01-20', 'Sophia', 'Lee', 'Female', '2024-01-17', '2024-01-22', 1, 32221),
(9, '2024-01-21', 'Robert', 'Williams', 'Male', '2024-01-19', '2024-01-24', 3, 32222),
(10, '2024-01-21', 'Emily', 'Davis', 'Female', '2024-01-18', '2024-01-23', 2, 32223);
-- Showing all outputs or informations of this table.
SELECT * FROM Library_Attendance;

-- Newid() function used to generate any random information
SELECT * FROM Library_Attendance
ORDER BY NEWID();

-- Altering  the Library_Management  table to increase the length of Lib_management_description
ALTER TABLE Library_Management 
ALTER COLUMN Lib_Management_description VARCHAR(MAX);

-- Inserting data into LibraryManagement Table
INSERT INTO Library_Management (Lib_management_id, Lib_management_name, Lib_management_description, Au_id, Genre_id) VALUES
(1, 'New Future Technology Studio', 'A studio for those who really like and love computer science or technology, exploring anything they want.', 4, 14),
(2, 'Time Travel: History in the Past', 'This book takes you through all past events, such as the lives of people and how they lived before.', 5, 15),
(3, 'Science Book Exhibition', 'An exhibition showcasing science-related books and knowledge.', 6, 16),
(4, 'Fantasy Fiction World', 'Immerse yourself in the magical realms of fantasy fiction with enchanting stories and mythical creatures.', 7, 17),
(5, 'Space Odyssey Collection', 'Embark on a cosmic journey with books that explore the wonders of space and the mysteries beyond our planet.', 8, 18),
(6, 'Romantic Escapade', 'Indulge in heartwarming love stories and romantic adventures that will sweep you off your feet.', 9, 19),
(7, 'Biographies of Influential Minds', 'Discover the inspiring life stories of remarkable individuals who shaped history and left a lasting legacy.', 10, 20),
(8, 'Self-Help Hub', 'Explore self-help books that provide valuable insights and practical advice for personal growth and empowerment.', 11, 21),
(9, 'Poetry Showcase', 'Dive into the world of poetic expression with a diverse collection of verses that evoke emotions and stir the soul.', 12, 22),
(10, 'Thriller Zone', 'Get ready for an adrenaline-pumping experience with gripping thrillers that will keep you on the edge of your seat.', 13, 23);

-- Showing all outputs or informations of this table. 
SELECT * FROM Library_Management;



-- Newid() function used to generate any random information.
SELECT * FROM Library_Management
ORDER BY NEWID();


-- Step 4: We're going to make our own questions and answers using JOIN Function. 
-- Q1: I want to show the names of all students alon with their section names.

SELECT Students.St_firstname, Students.St_lastname, Sections.Sect_name
FROM Students 
JOIN Sections ON Students.Sect_id = Sections.Sect_id;

-- Q2: I want to list the titles and ISBN IDs of books along with the names of their authors. 

SELECT Books.Bk_title, Books.Bk_ISBN_id, Authors.Au_name
FROM Books
JOIN Authors ON Books.Au_id = Authors.Au_id;

-- Q3: I want to know the names of teachers along with the names of the classes they teach. 
SELECT Teachers.Tea_firstname, Teachers.Tea_lastname, Classes.Cl_name
FROM Teachers
JOIN Sections ON Teachers.Sect_id = Sections.Sect_id
JOIN Classes ON Sections.Cl_id = Classes.Cl_id;

-- Q4: I want to know the names of students who attended the library on a specific date. 
SELECT Library_Attendance.Lib_attend_St_firstname, Library_Attendance.Lib_attend_St_lastname
FROM Library_Attendance
JOIN Students ON Library_Attendance.St_id = Students.St_id
WHERE Lib_attend_date = '2024-01-17';

-- Q5: I want to know the names of books along with their generes. 
SELECT Books.Bk_title, Genres.Genre_name
FROM Books  JOIN Genres ON Books.Genre_id = Genres.Genre_id;

Step 5: I'm going to show you the table diagram of all objects and entities here.
![school_library_entity_relationship](https://github.com/AuntBawHein/School_Library_Management_System_SQL/assets/150255399/7faf02c5-241d-4916-b18a-e10788113836)


Step 6: I’m going to show you SQL Car Rental Management System Project database.
 [school_library_management_system_project_database_ms_words.docx](https://github.com/AuntBawHein/School_Library_Management_System_SQL/files/14392032/school_library_management_system_project_database_ms_words.docx)


Thank you very much. 






