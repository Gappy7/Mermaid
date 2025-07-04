# Documentation de l'API MCP Compression

## Introduction

L'API MCP Compression est un service FastAPI pour la compression et décompression de fichiers, images et vidéos. Cette documentation liste tous les endpoints disponibles avec des exemples d'utilisation via curl.

## Informations Générales

- **URL de Base**: `http://localhost:8000`
- **Documentation Interactive**: 
  - Swagger UI: `/docs`
  - ReDoc: `/redoc`

## Endpoints

### 1. Informations de Base

#### 1.1 Accueil
```
GET /
```
Retourne les informations de base sur l'API.

**Exemple:**
```bash
curl -X GET "http://localhost:8000/"
```

#### 1.2 Vérification d'état
```
GET /health
```
Vérifie l'état de l'API et retourne des informations sur les dossiers de travail.

**Exemple:**
```bash
curl -X GET "http://localhost:8000/health"
```

### 2. Gestion des Fichiers

#### 2.1 Liste des fichiers
```
GET /files
```
Liste tous les fichiers disponibles (uploadés et compressés).

**Exemple:**
```bash
curl -X GET "http://localhost:8000/files"
```

#### 2.2 Téléchargement de fichier
```
GET /download/{filename}
```
Télécharge un fichier spécifique par son nom.

**Paramètres:**
- `filename`: Nom du fichier à télécharger

**Exemple:**
```bash
curl -X GET "http://localhost:8000/download/compressed_1751622199_0321bb69.zip" -o fichier_local.zip
```

#### 2.3 Suppression de fichier
```
DELETE /files/{filename}
```
Supprime un fichier ou dossier spécifique.

**Paramètres:**
- `filename`: Nom du fichier à supprimer

**Exemple:**
```bash
curl -X DELETE "http://localhost:8000/files/compressed_1751622199_0321bb69.zip"
```

### 3. Compression

#### 3.1 Formats supportés
```
GET /formats
```
Retourne les formats de compression supportés par l'API.

**Exemple:**
```bash
curl -X GET "http://localhost:8000/formats"
```

#### 3.2 Compression de fichiers
```
POST /compress/files
```
Compresse un ou plusieurs fichiers dans une archive.

**Paramètres:**
- `files`: Liste des fichiers à compresser (multipart/form-data)
- `compression_type`: Type de compression (zip, tar, gzip, bz2, 7z) (défaut: zip)
- `compression_level`: Niveau de compression 1-9 (défaut: 6)
- `password`: Mot de passe pour protéger l'archive (optionnel)

**Exemple:**
```bash
curl -X POST "http://localhost:8000/compress/files?compression_type=zip&compression_level=6" \
  -F "files=@chemin/vers/fichier1.pdf" \
  -F "files=@chemin/vers/fichier2.pdf"
```

**Exemple avec mot de passe:**
```bash
curl -X POST "http://localhost:8000/compress/files?compression_type=zip&compression_level=6&password=motdepasse123" \
  -F "files=@chemin/vers/fichier1.pdf" \
  -F "files=@chemin/vers/fichier2.pdf"
```

#### 3.3 Compression d'Images
```
POST /compress/images
```
Compresse une ou plusieurs images.

**Paramètres:**
- `files`: Liste des images à compresser (multipart/form-data)
- `quality`: Qualité de compression (1-100) (défaut: 75)
- `max_width`: Largeur maximale (redimensionnement proportionnel) (optionnel)
- `max_height`: Hauteur maximale (redimensionnement proportionnel) (optionnel)
- `format_out`: Format de sortie (auto, jpg, png, webp) (défaut: auto)

**Exemple:**
```bash
curl -X POST "http://localhost:8000/compress/images" \
  -H "accept: application/json" \
  -F "quality=75" \
  -F "max_width=800" \
  -F "files=@chemin/vers/image1.jpg" \
  -F "files=@chemin/vers/image2.png"
```

#### 3.4 Compression de Vidéos
```
POST /compress/videos
```
Compresse une ou plusieurs vidéos.

**Paramètres:**
- `files`: Liste des vidéos à compresser (multipart/form-data)
- `quality`: Qualité de compression (low, medium, high) (défaut: medium)
- `resolution`: Résolution de sortie (720p, 480p, 360p) (optionnel)
- `audio_bitrate`: Bitrate audio (128k, 192k, etc.) (optionnel)
- `format_out`: Format de sortie (auto, mp4, webm) (défaut: auto)

**Exemple:**
```bash
curl -X POST "http://localhost:8000/compress/videos" \
  -H "accept: application/json" \
  -F "quality=medium" \
  -F "resolution=480p" \
  -F "files=@chemin/vers/video1.mp4" \
  -F "files=@chemin/vers/video2.mov"
```

### 4. Décompression

#### 4.1 Décompression de fichier
```
POST /decompress
```
Décompresse une archive.

**Paramètres:**
- `file`: Fichier archive à décompresser (multipart/form-data)
- `password`: Mot de passe si l'archive est protégée (optionnel)
- `extract_to`: Dossier de destination (optionnel)

**Exemple:**
```bash
curl -X POST "http://localhost:8000/decompress" \
  -F "file=@chemin/vers/archive.zip"
```

**Exemple avec mot de passe:**
```bash
curl -X POST "http://localhost:8000/decompress?password=motdepasse123" \
  -F "file=@chemin/vers/archive.zip"
```

## Scripts de Test

Pour tester rapidement les fonctionnalités de l'API, plusieurs scripts shell sont disponibles:

1. **test_api.sh**: Test complet de l'API (compression, décompression, liste de fichiers, etc.)
2. **test_compress.sh**: Test spécifique pour la compression de fichiers
3. **test_decompress.sh**: Test spécifique pour la décompression de fichiers
4. **test_images.sh**: Test spécifique pour la compression d'images
5. **test_media.sh**: Test complet pour la compression d'images et de vidéos
6. **test_password.sh**: Test de compression/décompression avec protection par mot de passe

### Exécution des Scripts

```bash
# Démarrer le serveur API
cd backend
python main.py

# Dans un autre terminal, exécuter les tests
cd /Users/ho.agirard/Desktop/mcp-compression
bash test_media.sh
```

## Formats Supportés

### Images
- JPEG/JPG
- PNG
- WebP
- GIF
- BMP
- TIFF

### Vidéos
- MP4
- MOV
- AVI
- MKV
- WebM
- MPEG

### Compression d'Archives
- ZIP
- TAR
- GZIP
- BZ2
- 7Z

## Notes d'utilisation

1. Avant de compresser des vidéos, assurez-vous que FFmpeg est installé sur le système.
2. Pour les images de grande taille, utilisez les paramètres `max_width` et `max_height` pour les redimensionner.
3. Pour une compression plus efficace des vidéos, vous pouvez ajuster la qualité et la résolution.
4. Les fichiers compressés sont stockés dans le dossier `compressed` à la racine du projet.
5. Les fichiers uploadés sont stockés temporairement et supprimés après traitement.
