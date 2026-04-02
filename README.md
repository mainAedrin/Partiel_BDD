Rendu
Question 2 : 
SELECT CONCAT(a.prenom, ' ', UPPER(a.nom)) AS "Sportif"
FROM athlete a
INNER JOIN participation p ON a.id_athlete = p.id_athlete
GROUP BY a.id_athlete, a.prenom, a.nom
HAVING COUNT(p.id_epreuve) >= 2;

Question 1:
SELECT a.nom AS 'Nom Athlète', e.nom AS "Nom de l'épreuve", AVG(n.valeur) AS note_finale
FROM athlete a
INNER JOIN run r ON a.id_athlete = r.id_athlete
INNER JOIN epreuve e ON r.id_epreuve = e.id_epreuve
INNER JOIN note n ON r.id_run = n.id_run
GROUP BY a.nom, e.nom;

Question 3: 
SELECT a.nom AS "Nom de l'athlète", p.nom AS "Pays"
FROM athlete a
INNER JOIN pays p ON a.id_pays = p.id_pays
INNER JOIN participation part ON a.id_athlete = part.id_athlete
WHERE (part.id_athlete, part.id_epreuve) NOT IN (
    SELECT id_athlete, id_epreuve 
    FROM run
);
Je crois que la table particiaption me permet de faire le lie nmais quand j'execute ma requête je n'ai aucun retour.

Question 5:
DELIMITER // 
CREATE TRIGGER trg_ajouter_note
BEFORE INSERT ON note
FOR EACH ROW
BEGIN
	IF NEW.valeur < 0 OR NEW.valeur > 100 THEN
    SIGNAL SQLSTATE '45000'
    SET MESSAGE_TEXT = 'La note doit être comprise entre 0 et 100';
    END IF;
END; //

DELIMITER ;

BONUS : 
Les améliorations possibles seraient de faire des procédures stockées qui donnerait le classement par pays par exemple.
Elle pourrait être améliorée en vue des JO en ajoutant les médailles obtnues/les médailles par pays.
