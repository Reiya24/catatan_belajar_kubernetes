# rollback deployment

## kubernetes rollout

- kubectl rollout history object name > melihat history rollout
- kubectl rollout pause object name > menandai sebagai pause
- kubectl rollout resume object name > resume pause
- kubectl rollout restart object name > merestart rollout
- kubectl rollout status object name > melihat status rollout
- kubectl rollout undo object name > undo ke rollout sebelumnya

tidak semua object di kubernetes mendukung rollout

![Untitled](rollback%20deployment%204c9e34f6327d4ce6bfebae4ae55a1f56/Untitled.png)