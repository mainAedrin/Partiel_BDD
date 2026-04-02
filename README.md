Rendu

Question 2 : 
SELECT CONCAT(a.prenom, ' ', UPPER(a.nom)) AS "Sportif"
FROM athlete a
JOIN participation p ON a.id_athlete = p.id_athlete
GROUP BY a.id_athlete, a.prenom, a.nom
HAVING COUNT(p.id_epreuve) >= 2;
