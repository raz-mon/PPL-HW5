% Signature: author(_Id, _Name)/2.
% Purpose: _ is an author, with ID id.
author(1, "Isaac Asimov").
author(2, "Frank Herbert").
author(3, "William Morris").
author(4, "J.R.R Tolkein").
author(abc, gulko).
author(def, yevgeny).

% Signature: genre(_Id, _Name)/2.
% Purpose: _Name is a name of a genre, with ID _ID.
genre(1, "Science").
genre(2, "Literature").
genre(3, "Science Fiction").
genre(4, "Fantasy").
genre(202, math).
genre(203, physics).

% Signature: book(_Name, _AuthorId, _GenreId, _Length)/4 
% Purpose: _Name is a book, written by an author with id _AuthorID, from genre _GenreID, and length _Length.
book("Inside The Atom 1", 1, 1, 500).
book("Inside The Atom 2", 1, 1, 505).
book("Inside The Atom 3", 1, 1, 510).
book("Asimov's Guide To Shakespeare", 1, 2, 400).
book("I, Robot", 1, 3, 450).
book("You, Not Robot", 1, 3, 550).
book("Dune", 2, 3, 550).
book("The Well at the World's End", 3, 4, 400).
book("The Hobbit", 4, 4, 250).
book("Star War", 4, 3, 250).
book("The Hobbit", 4, 4, 250).
book("The Hobbit", 4, 4, 250).
book("The Lord of the Rings", 4, 4, 1250).
book("The Lord of the Rings - Perturbration Theory", 4, 1, 1250).
book(calculus, abc, 202, 500).
book(physics-3, def, 203, 100).
book(linear-algebra, abc, 202, 400).
book(probability, abc, 202, 300).
book(thermodynamic, def, 203, 200).

% Signature: authorOfGenre(GenreName, AuthorName)/2
% Purpose: AuthorName written a book belonging to the genre GenreName
authorOfGenre(GenreName, AuthorName) :- 
    genre(GenreId, GenreName), author(AuthorId, AuthorName), book(_Name,AuthorId,GenreId, _Length).

% Signature: longestBook(AuthorId, BookName)/2
% Purpose: true if BookName is the longenst book of the author with id AuthorId
longestBook(AuthorId, BookName) :-
    book( BookName , AuthorId, _, L),
    findall(Length, book( _ , AuthorId, _, Length), Bag),
    max_list(Bag,L).

% Signature: versatileAuthor(AuthorName)/1
% Purpose: true if AuthorName wrote books from at least three diffrenet genre
versatileAuthor(AuthorName) :- author(AuthorId, AuthorName),
    							findall(GenreId, book(_, AuthorId, GenreId, _), Bag),
    							atLeastThree(Bag).

atLeastThree(X) :- append([_, [R], _, [O], _, [P], _], X), R \= O, R \= P, O \= P. 









