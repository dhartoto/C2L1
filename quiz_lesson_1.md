1. Why do they call it a relational database?
A: Because tables can be associated to each other

2. What is SQL?
A. Structured Query Language is a language used to query and manage the database.

3. There are two predominant view into a relational database. Wat are they, and how are they different?
A: There is the schema view and the data view. The schema view gives you the name of each attribute,
   the type of values it accepts. The data view shows you the name of the columns and the data within the columns.

4. In a table, what do we call the column that serves as the main identifier for a row of data? We're looking for
   the general database term, not the column names.
A: We call them attributes.

Incorrect! Answer: We call this the "primary key".

5. What is a foreign key, and how is it used?
A: A foreign key is an integer that links a row of data within a table with another table.

Additional from solutions: It's the identifier that connects an association with the models involved. It's
                           Always on the many side.

6. At a high level, describe the ActiveRecord pattern. This has nothing to do with Rails, but the actual pattern
   that ActiveRecord uses to perform its ORM duties.
A: ActiveRecord patterns link an object and its attributes to tables and columns within a database. It abstracts away
    the need to write SQL and allows the user to deal with the database in an object oriented way.

Additional from solutions: An object of that class is created as a row in the table. We can perform CRUD operations on 
                            the objects. 

7. If there's an ActiveRecord model called "CrazyMonkey", what should the table name be?
A: crazy_monkeys

8. If I'm building a 1:M association between Project and Issue, what will the model association and foreign key be?
  
  class Project < ActiveRecord::Base
    has_many :issues
  end

  class Issue < ActiveRecord::Base
    belongs_to :project
  end
  The foreign key will be in the issues table with the column name of 'project_id'

9. Given this code:

class Zoo < ActiveRecord::Base
  has_many :animals
end
  
  What do you expect the other model to be and what does the database schema look like?
  A:
  class Animal < ActiveRecord::Base
    belongs_to :zoo
  end

  What are the methods that are now available to a zoo to call related to animals?
  A: zoo.animals.all - return all the animal objects
     zoo.animals.destroy_all - removes the link between zoo and animals.
     zoo.animals.create - Add and save a new row in the animals table by mass-assignment.

  How do I create an animal called "jumpster" in a zoo called "San Diego Zoo"?
  A: Zoo.create(name: "San Diego Zoo")
     Animal.create(name: "jumpster", zoo_id: 1)

10. What is mass assignment? What's the non-mass assignment way of setting values?
A:  Mass assignment is the ability to assign multiple values to attributes at once.
Additional from solutions: with only a single assignment operator.

    Non-mass assignment:
    article = Article.new
    article.name = 'Article Name'
    article.save

11. What does this code do? Animal.first
A:  Selects the the first row of data from the animals table.

12. If I have a table called "animals" with columns called "name", and a model called Animal, 
    how do I instantiate an animal object with names set to "Joe". Which methods makes sure it
    saves to the database?
A:  Animal.create(name: "Joe")

13. How does a M:M association work at the database level?
    There is a join table that stores two foreign keys. One for each table on the many side.

14. What are the two ways to support a M:M association at the ActiveRecord model level? 
    Pros and cons of each approach?
    One way is to use the has_and_belongs_to_many method. The benefit of this is just that it requires less code
    i.e. a join table model is not required. The con is that you cannot add additional attributes to the join table.

    The second method is to use the has_many :through method. While a join table model is required it allows for
    additional attributes in the join table and therefore more flexible.

15. Suppose we have a User model and a Group model, and we have a M:M association all set up.
    How do we associate the two?
    class User < ActiveRecord::Base
      has_many :groups_users, foreign_key 'user_id'
      has_many :groups, through: :groups_users
    end

    class Group < ActiveRecord::Base
      has_many :groups_users, foreign_key 'group_id'
      has_many :users, through: :groups_users
    end

    class GroupsUsers < ActiveRecord::Base
      belongs_to :user
      belongs_to :group
    end