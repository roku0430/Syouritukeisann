// 【デプロイ時にこの行を置き換える必要があります！】
// const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
// const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};

// ↓↓↓ あなたのFirebase設定例 ↓↓↓
const appId = 'your-unique-app-id-for-firestore'; // 任意のユニークなID
const firebaseConfig = {
    apiKey: "AIzaSy...",
    authDomain: "your-project.firebaseapp.com",
    projectId: "your-project-id",
    storageBucket: "...",
    messagingSenderId: "...",
    appId: "1:...",
};
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // 全てのドキュメントに適用されるルール
    match /artifacts/{appId} {
      // ユーザーデータは認証済みのユーザーIDに基づいて読み書きを許可
      match /users/{userId}/{document=**} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }
  }
}
