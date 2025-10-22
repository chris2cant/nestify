# AGENTS.md - Pratiques de Développement

Ce document définit les pratiques de développement et les conventions utilisées dans ce projet.

## 🚀 Gestion des Commits

### Format des Messages de Commit

- **Format** : `type(scope): description`
- **Exemple** : `feat(react-core-components): add new button component`
- **Règle spéciale** : Pour les packages dans `/packages/*`, inclure le nom du package
  - Exemple : `feat(react-core-components)` pour `@classify/react-core-components` dans `./packages/classify/react-core-components/*`
- **Langue** : Toujours en anglais

### Types de Commits

- `feat`: Nouvelle fonctionnalité
- `fix`: Correction de bug
- `docs`: Documentation
- `style`: Formatage, point-virgules manquants, etc.
- `refactor`: Refactoring du code
- `test`: Ajout ou modification de tests
- `chore`: Tâches de maintenance

## 🎯 Règles de Code

### Fonctions et Lisibilité

- **Préférer** les fonctions explicites et lisibles, même en chaîne
- **Autoriser** le chaînage uniquement si ≤3 appels et sans effets de bord
- **Extraire** une fonction nommée si le code dépasse 5 lignes ou nécessite une explication
- **Utiliser** des noms explicites : verbe + domaine (ex: `formatInvoiceDate`, `fetchUserProfile`)

### Organisation des Composants React

Ordre obligatoire dans les composants :

1. **Props** - Interface des propriétés
2. **useState / useReducer** - Gestion d'état
3. **Handlers** - Fonctions de gestion d'événements
4. **useEffect** - Effets de bord
5. **JSX** - Rendu du composant

### Hooks et Effets de Bord

- Les hooks ne doivent **pas** encapsuler d'effets de bord implicites
- Garder les interfaces `Props` dans le fichier du composant
- Centraliser les autres types dans `types/`, éviter les dépendances circulaires

### Styling

- **Préférer** `styled` plutôt que `sx` pour les styles
- **Nommer** le composant styled racine `Root`
- **Éviter** de chaîner plus de 3 fonctions ou des fonctions avec effets de bord

### Documentation

- **Ne pas ajouter** de commentaires dans le code
- La documentation doit être dans des fichiers dédiés (README, docs, etc.)

## 🛠️ Outils et Commandes

### Gestionnaire de Paquets

- **Utiliser** `yarn` comme gestionnaire de paquets principal

### Composants UI

- **Utiliser en priorité** les composants de la librairie `@classify/react-core-components` quand ils existent

### Commandes Système

- **Utiliser** `yes |` avant les commandes `cp`, `rm`, `mv` etc. pour valider la double confirmation
  - Exemple : `yes | cp file1 file2`

## 🌍 Langue et Communication

- **Toujours répondre** en français dans la documentation et les communications
- Les messages de commit restent en anglais (voir section commits)

## 📁 Structure du Projet

```
/packages/*          # Packages avec conventions de nommage spécifiques
/types/              # Types centralisés
/components/          # Composants réutilisables
```

## 🔄 Workflow Git

1. Créer une branche feature : `git checkout -b feature/nom-feature`
2. Commiter avec le format défini
3. Pousser vers le dépôt distant
4. Créer une Pull Request

## 📝 Exemples

### Commit Correct

```bash
git commit -m "feat(react-core-components): add loading state to button component"
```

### Structure de Composant

```typescript
interface Props {
  title: string;
  onClick: () => void;
}

const MyComponent = ({ title, onClick }: Props) => {
  const [isLoading, setIsLoading] = useState(false);

  const handleClick = () => {
    setIsLoading(true);
    onClick();
  };

  useEffect(() => {
    // Effet de bord
  }, []);

  return (
    <Root>
      <button onClick={handleClick}>{title}</button>
    </Root>
  );
};
```

---

_Ce document est vivant et doit être mis à jour selon l'évolution des pratiques du projet._
