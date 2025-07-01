![get_next_line](https://github.com/user-attachments/assets/050bb54f-d66f-448b-a118-43f0fe008005)

# Sujet :
Le projet get_next_line a pour but d'écrire une fonction capable de lire ligne par ligne à partir d’un descripteur de fichier donné. <br>
Chaque appel à get_next_line retourne la ligne suivante lue depuis le fichier, y compris le \n s'il est présent, jusqu'à ce qu'il n'y ait plus rien à lire (EOF). <br>

# Fonctionnement :
- Utilise la fonction read() pour lire depuis un descripteur de fichier (fd)
- Lecture en blocs de BUFFER_SIZE octets (défini dans le header)
- Utilise une variable statique pour conserver les données entre les appels
- Retourne NULL à la fin du fichier ou en cas d’erreur

# Fonctions utilisées :
`static char *read_line(int fd, char *line)`
- Lit et accumule les caractères jusqu’à \n ou EOF
- Utilise un buffer temporaire (BUFFER_SIZE)
- Concatène les lectures successives via ft_strjoin
- Gère les erreurs et libérations mémoire en cas de read() == -1

`static char *next_line(char	*line)`
- Extrait la ligne suivante à partir du contenu déjà lu
- Localise le \n et duplique ce qui le suit pour le prochain appel
- Coupe proprement la chaîne pour isoler la ligne à retourner

`char *get_next_line(int fd)`
- Gère un buffer statique (persistant) pour chaque appel
- Appelle read_line() pour lire une ligne complète
- Prépare la ligne suivante avec next_line()

# Bonus :
- Le comportement est extensible pour plusieurs fichiers simultanés via FD_MAX

# Exemple d'affichage :
Exemple (contenu de test.txt) : <br>
bonjour
hello
comment

Appels successifs à get_next_line(fd) va retourner :  <br>
"bonjour\n"
"hello\n"
"comment"
