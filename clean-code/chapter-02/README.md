# Chapter02
## Naming

### 1. Name should tell the intent
- Why it exists, what it does and how to use it
- E.g. good name would be **employeePyamentInfo** vs **ePay**

### 2. Avoid confusing names
- Using names that already imply something!
- E.g. naming something unix, testList (even if it's not a list)

### 3. Choose clear names
- Say what you mean and mean what you say
- E.g. **deleteItems** over **bustThemDown**, **kill** over **whack**

### 4. Use good distinctions + Avoid using number at end!
- Use distinctions that make sense and thus don't just use numbers
- E.g. don't use **list1**, **list2**, use **productIds**, **productDetails**, etc
- E.g. using **productInfo** and **productDetails** - means same and distinction is harder between these two variables.

### 5. Use pronounceable names
- Programming is a social activity
- E.g. don't use variable name as **dobyymm** for **DateOfBirthInYearsMonths**

### 6. Use searchable names
- E.g. don't name variable as **e**, **z**, etc. Use **Event**, **Max_Students**, etc

### 7. Don't encode types in names
- Remember containers of variables can change
- E.g. **phoneString**, **paymentInt**, etc are bad names, payment can be made **float** in future and thus the name also has to now change.

### 8. Avoid prefix to names
- E.g. **m_description** -> **member_description** (easier to understand)
- E.g. Don't use **IShapeFactory** to mean it is an interface, use **ShapeFactory** and **ShapeFactoryImpl**

### 9. Class names - nouns + Function names - verbs
- E.g. Class names - **student**, **car**, **employee**, etc
- E.g. Function names - **postPayment**, **deletePage**, etc

### 10. Use names consistently
- Pick one concept and stick to it
- E.g. use **controller** everywhere instead of using **manager** and **controller** used interchangeably / **driver** and **controller** used in same place

### 11. Don't use same name to mean two different things
- E.g. **payInfo** represents amount to pay and **payInfo** also represents who to pay and bank info. Should use **employeePaymentAmount** and **employeeBankDetails**

### 12. Use Domain specific names
- Remember your code is going to be read by computer engineers, helps them give context quickly
- E.g. **accountVisitor** (indicating visitor pattern), **jobQueue** - (indicating a queue), **nameBuilder** (indicating a builder).

### 13. Avoid too long names
