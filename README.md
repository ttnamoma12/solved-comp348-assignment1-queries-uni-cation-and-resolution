Download Link: https://assignmentchef.com/product/solved-comp348-assignment1-queries-uni-cation-and-resolution
<br>
In this assignment you will be practicing logical programming using Prolog language. This assignment consists of three parts: 1) Fact representation, 2) Queries, Uni cation, and Resolution, and 3) Implementation Exercises.

Note that Part 1 of the assignment is due on May 10<sup>th </sup>and is to be submitted separately.

See section 5 for more details.

Your assignment is given in three parts, as follows. 1) Fact representation, which is to be submitted separately, 2) Queries, Uni cation, and Resolution, and 3) Implementation Exercises, all of which will be demoed by the whole team.

<h2><a name="_Toc8637"></a>2.1            Fact Representation</h2>

Provide a knowledge-base of clauses specifying your class schedule in prolog, as demonstrated in the following.

team([&lt;&lt;student-ids&gt;&gt;…]). student_info(’&lt;&lt;student-id&gt;&gt;’, ’&lt;&lt;first-name&gt;&gt;’, ’&lt;&lt;last-name&gt;&gt;’).

takes_course(’&lt;&lt;student-id&gt;&gt;’, ’&lt;&lt;course-name&gt;&gt;’, ’&lt;&lt;course-number&gt;&gt;’, ’&lt;&lt;course-section&gt;&gt;’).

course_schedule(’&lt;&lt;course-name&gt;&gt;’, ’&lt;&lt;course-number&gt;&gt;’,

’&lt;&lt;course-section&gt;&gt;’, ’&lt;&lt;dow&gt;&gt;’, ’&lt;&lt;from-time&gt;&gt;’, &lt;&lt;to-time&gt;&gt;’). dow is day of week: ‘sun’, ‘mon’, ‘tue’, ‘wed’, ‘thu’, ‘fri’, and ‘sat’.

from-time and to-time are class start and end in military format, i.e. 0845 (8:45am), 1445 (2:45pm), etc.

course-name, course-number, and course-section are all in lower case: e.g.. comp 348 aa

Below is a sample knowledge-base for a group of two: John Doe and Jane Doe. Note that in this question, using single quote (<sup>’</sup>) is mandatory.

team([’4000123’, ’4000228’]).

student_info(’4000123’, ’John’, ’Doe’). student_info(’4000228’, ’Jane’, ’Doe’). takes_course(’4000123’, ’comp’, ’348’, ’aa’). takes_course(’4000123’, ’comp’, ’348’, ’aaae’). takes_course(’4000228’, ’comp’, ’348’, ’ab’). takes_course(’4000228’, ’comp’, ’348’, ’abaf’). takes_course(’4000228’, ’comp’, ’346’, ’cc’). course_schedule(’comp’, ’348’, ’aa’, ’mon’, ’1445’, ’1715’). course_schedule(’comp’, ’348’, ’aa’, ’wed’, ’1445’, ’1715’). course_schedule(’comp’, ’348’, ’aaae’, ’mon’, ’1345’, ’1405’). course_schedule(’comp’, ’348’, ’aaae’, ’wed’, ’1345’, ’1405’). course_schedule(’comp’, ’348’, ’ab’, ’tue’, ’1315’, ’1545’). course_schedule(’comp’, ’348’, ’ab’, ’thu’, ’1315’, ’1545’). course_schedule(’comp’, ’348’, ’abaf’, ’tue’, ’1615’, ’1705’). course_schedule(’comp’, ’348’, ’abaf’, ’thu’, ’1615’, ’1705’). course_schedule(’comp’, ’346’, ’cc’, ’tue’, ’1830’, ’2100’). course_schedule(’comp’, ’346’, ’cc’, ’thu’, ’1830’, ’2100’).

John is taking one course (comp 348 aa + the tutorial aaae) and Jane is taking two courses (comp 348 ab + the tutorial abaf we well as comp 346 cc with no tutorial). Note that both courses are scheduled on multiple days.

Q 1. Provide the knowledge-base of ALL courses for ALL members of the team. Create a le named ‘schedule-studid.pl’ where studid is the id of the leader of the team. Include all clauses in the le. Write every clause in a single line. One le per group. Submit this separately (see submission notes).

Q 2. Run the following query and report the result:

team(X), member(S, X), findall(S, takes_course(S, _, _, _), LL), length(LL, NN), write(S), write(’ has only taken ’), write(NN),

write(’ courses and tutorials in summer 2020.’), nl, fail.

Is the above information correct?

The above must be submitted in stage 1 (see submission notes for details).

Q 3. Create below mentioned rules to query the designation information from your knowlegebase.

Hint: Use the cut operator where applicable.

all_sections(CNAM, CNUM, L) :- …

/* L contains a list of all sections of course CNAME, CNUM,

i.e. calling all_sections(’comp’, ’348’, L) will result in L=[’aa’, ’ab’];

no duplicates */

has_taken(S, [CNAM|[CNUM|[SEC|[]]]]) :- …

/* true if student S takes the course CNAM CNUM SEC,

e.g. takes(’4000123’, [’comp’, ’348’, ’aa’]) */

has_taken2(S, [CNAM|[CNUM|[]]]) :- …

/* true if S takes any sections of the course CNAM CNUM,

e.g. takes(’4000123’, [’comp’, ’348’]) */

all_subjects(S, L) :- …

/* L contains all the courses subjects that have been taken by student S, i.e. [’comp’, ’soen’]; no duplicates */

all_courses(S, L) :- …

/* L contains all the courses that have been taken by student S, i.e. all_courses(’4000123’, L) will result in

L=[[’comp’, ’348’, ’aa’], [’comp’, ’348’, ’ab’]] */

all_courses2(S, L) :- …

/* similar to all_courses but without section info;

no duplicates */

Q 4. Modify the code in Q2 to count only the courses regardless of their sections (i.e. comp 348 aa and aaae will be counted as one)

Q 5. Compare the result for all_courses2(’4000123’, L) vs. all_courses2(4000123, L). Explain the di erence.

<h2><a name="_Toc8638"></a>2.2            Queries, Uni cation, and Resolution</h2>

Q 6. Uni cation: Indicate which of the following pairs of terms can be uni ed together? If they can’t be uni ed, please provide the reason for it. In case of error, indicate the error. If they can be uni ed successfully, wherever relevant, provide the variable instantiations that lead to successful uni cation. (Note that ‘=’ indicates uni cation)

<ol>

 <li>food(bread, X) = Food(Y, soup)</li>

 <li>Bread = soup</li>

 <li>Bread = Soup</li>

 <li>food(bread, X, milk) = food(Y, salad, X)</li>

 <li>manager(X) = Y</li>

 <li>meal(healthyFood(bread), drink(milk)) = meal(X,Y)</li>

 <li>meal(eat(Z), drink(milk)) = [X]</li>

 <li>[eat(Z), drink(milk)] = [X, Y | Z]</li>

 <li>f(X, t(b, c)) = f(l, t(Z, c))</li>

 <li>ancestor(french(jean), B) = ancestor(A, scottish(joe))</li>

 <li>meal(healthyFood(bread), Y) = meal(X, drink(water))</li>

 <li>[H|T] = [a, b, c]</li>

 <li>[H, T] = [a, b, c]</li>

 <li>breakfast(healthyFood(bread), egg, milk) = breakfast(healthyFood(Y), Y, Z)</li>

 <li>dinner(X, Y, Time) = dinner(jack, cook( egg, oil), Evening)</li>

 <li>k(s(g), Y) = k(X, t(k))</li>

 <li>equation(Z, f(x, 17, M), L*M, 17) = equation(C, f(D, D, y), C, E)</li>

 <li>a(X, b(c, d), [H|T]) = a(X, b(c, X), b)</li>

</ol>

Q 7. Queries: Assume we have the following database in a Prolog program:

course(hit_transfer, mechanical).

course(web_design,computer).

course(design_methods, fine-arts).

course(poetry, literature). course(leadership, management). course(biology,medicin). lab_number(mechanical,15). lab_number(fine_arts,10). lab_number(X, Z) :-course(X, Y), lab_number(Y, Z). field(mechanical,engineering). field(computer, engineering).

field(fine-arts, art). field(literature, social). field(management, buisiness).

field(X, Y) :- course(X, Z), field(Z, Y). student(anna, hit_transfer). student(daniel, hit_transfer). student(adrian, web_design). student(ava, design_methods).

student(jack, poetry). student(lee, leadership).

student(X, Y) :- field(Z, Y), student(X, Z). student(X):- student(X,_).

Determine the type of each of the following queries (ground/non-ground), and explain what will Prolog respond for each of these queries (write all the steps of uni cations and resolutions for each query)?

<ol>

 <li>? field(hit_transfer,engineering).</li>

 <li>? lab_number(fine_arts,X).</li>

 <li>? field(computer, literature).</li>

 <li>? course(X,Y).</li>

 <li>? student(adrian).</li>

 <li>? student(anna, engineering).</li>

 <li>? student(X, engineering).</li>

 <li>? student(X,fine-arts), course(fine_arts, Y).</li>

 <li>? field(_,X).</li>

 <li>? lab_number(_,X), field(X,Y).</li>

 <li>? lab_number(X,15), field(X,Y).</li>

 <li>? student(X), !, student(X,_).                % note to cut here</li>

 <li>? student(X), student(X,_), !.</li>

 <li>? course(X,_), + student(_,X). % + is for negation (not)</li>

</ol>

Q 8. Uni cation, Resolution, and Backtracking: Assume, you are working with the following knowledge base:

house_elf(dobby). witch(hermione). witch(mcGonagall). witch(rita_skeeter). wizard(dobby). magic(X):- house_elf(X). magic(X):- wizard(X). magic(X):- witch(X).

Write the details of steps of search (uni cation, resolutions, and back tracking) and also the answer for each of the following queries:

? magic(Hermione).

? magic(hermione).

<h2><a name="_Toc8639"></a>2.3            Implementation Exercises</h2>

Q 9. Assume, you are working with the following knowledge base::

family(

person(john, cohen, date(17,may,1990), unemployed),

person(lily, cohen, date(9,may,1990), unemployed),[] ). family( person(john, armstrong, date(7,may,1988), unemployed), person(lily, armstrong, date(29,may,1961), unemployed),[]). family( person(eric, baily, date(7,may,1963), works( bbc, 2200)), person(grace, baily, date(9,may,1965), works( ntu, 1000)), [ person(louie, baily, date(25,may,1983), unemployed) ] ). family( person(eric, baily, date(7,may,1963), works( acc, 21200)), person(grace, baily, date(9,may,1965), works(ntnu, 12000)), [ person( louie, baily, date(25,may,1983), unemployed) ]). family( person(eric, fox, date(27,may,1970), works(bbc, 25200)), person(grace, fox, date(9,may,1971), works(ntbu, 13000)), [ person(louie, fox, date(5,may,1993), unemployed) ]). family( person(tom, cohen, date(7,may,1960), works( bcd, 15200)), person(ann, cohen, date(29,may,1961), unemployed),

[ person(pat, cohen, date(5,may,1983), works(bcd, 15200)),

person(jim, cohen, date(5,may,1983), works(bcd, 15200))]). family( person(bob, armstrong, date(12,oct,1977), works(ntnu, 12000)), person(liz,armstrong, date(6,oct,1975), unemployed),

[ person(bob, armstrong, date(6,oct,1999), unemployed),

person(sam,armstrong, date(8,oct,1998), unemployed) ]). family( person(tony, oliver, date(7,may,1960), works( bbc, 35200)), person(anny, oliver, date(9,may,1961), unemployed),

[ person(patty, oliver, date(8,may,1984), unemployed), person(jimey, oliver, date(5,may,1983), unemployed) ]). family( person(jack, fox, date(27,may,1940), unemployed), person(jane, fox, date(9,aug,1941), works( ntu, 13050)),

[ person(andy, fox, date(5,aug,1967), works(com, 12000)),

person(kai, fox, date(5,jul,1969), unemployed) ]).

husband(X) :- family( X, _, _). wife(X) :- family( _, X, _). child(X) :- family( _, _, Children), member(X, Children). exists(Person) :- husband(Person); wife(Person); child(Person). dateofbirth(person(_, _, Date, _), Date). salary(person(_, _, _, works(_, S)), S). salary(person(_, _, _, unemployed), 0).

<ol>

 <li>Write a prolog rule totalIncome/2 to compute the total income of a family.</li>

 <li>Write a prolog query to print total income of each family.</li>

 <li>Write a prolog query to print family details of each family that has income per familymember less than 2000.</li>

 <li>Write a prolog query to print family details of each family where children’s total incomeis more than their parents.</li>

</ol>

Q 10. The following circuit represents a half-adder where A and B are the inputs, and S and C represent the Sum and Carry bits, respectively.

<ol>

 <li>Implement the above circuit in prolog.</li>

 <li>Write the query to calculate the outputs for S and C for A = 0 and B = _. Provide theoutput.</li>

</ol>

Q 11. Write a Prolog query with arity 2 to return the rst <em>n </em>numbers of a Lucas sequence in a list.

<a href="https://brilliant.org/wiki/lucas-numbers/">https://brilliant.org/wiki/lucas-numbers/</a>

The Lucas sequence has the same recursive relationship as the Fibonacci sequence, where each term is the sum of the two previous terms, except that the rst two numbers in the sequence are: 2, and 1. The rst few elements of the sequence are: 2<em>,</em>1<em>,</em>3<em>,</em>4<em>,</em>7<em>,</em>11<em>,</em>18<em>,…</em>