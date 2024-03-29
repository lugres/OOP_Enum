# OOP_Enum
Using enumeration type and bitwise ops for user permissions, a refactored solution with decorators.

While exploring OOP in Python, I solved a challenge of using an enumerator type and bitwise operations for manipulating user permissions. Detailed requirements for the task are below. The second version of the solution uses decorators for checking users' permissions.

##################
## CHALLENGE 12 ##
##################

# Requirements:
 - Define a new type called Permission that stores user permissions: read, write, and/or execute
 - This type should be an enumeration, with the ability to support bitwise operations
 - Separately define a new type called User, which takes a name and user_role at instantiation
 - Internally, the User class sets a permissions attribute depending on the specified user_group:
   - admin: read, write, and execute
   - user: read,
   - manager: read, write
   - support: execute
 - The User class also implements (or ideally inherits) read(file), write(file, content), and execute(file) methods which
 are permission-checked, e.g. a User belonging to the support user_role will not be able to write, but only execute
 - For ease of operation, assume that the read/write/execute functionality pertains to a python script
 - Instances of User should have an informative string representation
 - As an extra challenge, try to allow some polymorphism in the user_role so that it's possible to instantiate by both
 string roles as well as integers, e.g. User("A", user_role=2) would imply WRITE-only permissions, whereas
 User("B", user_role=6) would imply WRITE and EXEC, because 2**1 + 2**2 = 2 + 4 = 6

 Example Usage:
 u1 = User(name="Aaron", user_role="user")
 u1
 User(name='Aaron', user_role='user')

 u2 = User("Andrew", "admin")
 u2.permissions
 <Permission.EXEC|WRITE|READ: 7>

 u2.write(file="script.py", content="for i in range(10): print(i)")
 u2.execute()
 0
 1
 2
 3
 4
 5
 6
 7
 8
 9

 u1.read(file="script.py")
 'for i in range(10): print(i)'

 u1.execute(file="script.py")
 PermissionError: User does not have EXEC permission

 u3 = User("Joseph", 6)
 u3.permissions
 <Permission.EXEC|WRITE: 6>

 u3.execute(file="script.py")
 0
 1
 2
 3
 4
 5
 6
 7
 8
 9
