# 🚀 Git Manuel - Kapsamlı Git Komutları Rehberi

> Git'in temel kavramlarından ileri seviye tekniklerine kadar kapsamlı Türkçe kılavuz

## 📖 İçindekiler

- [🔰 Git Temelleri](#-git-temelleri)
- [🌿 Branch (Dal) İşlemleri](#-branch-dal-işlemleri)
- [📤 Push ve Pull İşlemleri](#-push-ve-pull-işlemleri)
- [🔄 Merge ve Rebase](#-merge-ve-rebase)
- [📝 Commit İşlemleri](#-commit-işlemleri)
- [🔍 Geçmiş ve Log İşlemleri](#-geçmiş-ve-log-işlemleri)
- [🏷️ Tag İşlemleri](#️-tag-işlemleri)
- [🔧 Konfigürasyon](#-konfigürasyon)
- [⚡ İleri Seviye Komutlar](#-i̇leri-seviye-komutlar)
- [🛠️ Sorun Giderme](#️-sorun-giderme)
- [📊 Git Workflow Örnekleri](#-git-workflow-örnekleri)

---

## 🔰 Git Temelleri

### Repository Oluşturma ve Klonlama

```bash
# Yeni bir git repository'si başlatma
git init

# Mevcut bir repository'yi klonlama
git clone <repository-url>

# Belirli bir branch'i klonlama
git clone -b <branch-name> <repository-url>

# Shallow clone (sadece son commit)
git clone --depth 1 <repository-url>
```

### Dosya Durumu ve Staging

```bash
# Repository durumunu kontrol etme
git status

# Kısa format ile durum görme
git status -s

# Dosyaları staging area'ya ekleme
git add <dosya-adı>
git add .                    # Tüm dosyalar
git add *.js                 # Belirli uzantıdaki dosyalar
git add -A                   # Tüm değişiklikler (silinen dosyalar dahil)

# Staging area'dan dosya çıkarma
git reset HEAD <dosya-adı>
git restore --staged <dosya-adı>

# Dosyadaki değişiklikleri geri alma
git checkout -- <dosya-adı>
git restore <dosya-adı>
```

### Basic Commit İşlemleri

```bash
# Commit oluşturma
git commit -m "Commit mesajı"

# Staging ve commit'i birlikte yapma
git commit -am "Commit mesajı"

# Son commit'i düzenleme
git commit --amend -m "Yeni commit mesajı"

# Boş commit oluşturma
git commit --allow-empty -m "Empty commit"
```

---

## 🌿 Branch (Dal) İşlemleri

### Branch Oluşturma ve Yönetimi

```bash
# Mevcut branch'leri listeleme
git branch                   # Local branch'ler
git branch -r               # Remote branch'ler
git branch -a               # Tüm branch'ler

# Yeni branch oluşturma
git branch <branch-adı>

# Branch oluşturup geçiş yapma
git checkout -b <branch-adı>
git switch -c <branch-adı>   # Modern syntax

# Belirli bir commit'ten branch oluşturma
git checkout -b <branch-adı> <commit-hash>

# Remote branch'ten local branch oluşturma
git checkout -b <local-branch> origin/<remote-branch>
```

### Branch Geçişleri

```bash
# Branch'ler arası geçiş
git checkout <branch-adı>
git switch <branch-adı>      # Modern syntax

# Önceki branch'e geri dönme
git checkout -
git switch -

# Stash ile güvenli geçiş
git stash push -m "Geçici kayıt"
git checkout <branch-adı>
git stash pop               # Değişiklikleri geri getirme
```

### Branch Silme

```bash
# Local branch silme
git branch -d <branch-adı>   # Güvenli silme
git branch -D <branch-adı>   # Zorla silme

# Remote branch silme
git push origin --delete <branch-adı>
git push origin :<branch-adı>

# Silinen remote branch referanslarını temizleme
git remote prune origin
```

---

## 📤 Push ve Pull İşlemleri

### Push İşlemleri

```bash
# Değişiklikleri remote'a gönderme
git push origin <branch-adı>

# İlk push (upstream ayarlama)
git push -u origin <branch-adı>

# Tüm branch'leri push etme
git push --all origin

# Tag'leri push etme
git push --tags origin

# Zorla push (dikkatli kullanın!)
git push --force origin <branch-adı>
git push --force-with-lease origin <branch-adı>  # Güvenli versiyon
```

### Pull İşlemleri

```bash
# Remote'dan güncellemeleri çekme
git pull origin <branch-adı>

# Tüm remote branch'lerin güncellemelerini çekme
git fetch --all

# Rebase ile pull yapma
git pull --rebase origin <branch-adı>

# Specific remote'dan pull
git pull <remote-name> <branch-adı>
```

### Remote İşlemleri

```bash
# Remote repository'leri listeleme
git remote -v

# Remote ekleme
git remote add <remote-adı> <url>

# Remote URL'ini değiştirme
git remote set-url origin <yeni-url>

# Remote silme
git remote remove <remote-adı>

# Remote branch'leri güncelleme
git remote update
```

---

## 🔄 Merge ve Rebase

### Merge İşlemleri

```bash
# Branch'i mevcut branch'e merge etme
git merge <branch-adı>

# No-fast-forward merge
git merge --no-ff <branch-adı>

# Squash merge (tüm commit'leri tek commit'e çevirme)
git merge --squash <branch-adı>

# Merge conflict durumunda
git status                   # Çakışan dosyaları görme
# Dosyaları düzenleyin
git add <çözülen-dosya>
git commit                   # Merge commit'i tamamlama

# Merge'i iptal etme
git merge --abort
```

### Rebase İşlemleri

```bash
# Branch'i başka branch üzerine rebase etme
git rebase <base-branch>

# Interactive rebase (son 3 commit)
git rebase -i HEAD~3

# Rebase'i devam ettirme
git rebase --continue

# Rebase'i iptal etme
git rebase --abort

# Rebase sırasında conflict çözme
git add <çözülen-dosya>
git rebase --continue
```

### Cherry-pick

```bash
# Belirli bir commit'i mevcut branch'e uygulama
git cherry-pick <commit-hash>

# Birden fazla commit'i cherry-pick etme
git cherry-pick <commit1> <commit2>

# Range ile cherry-pick
git cherry-pick <start-commit>..<end-commit>
```

---

## 📝 Commit İşlemleri

### Commit Düzenleme

```bash
# Son commit mesajını değiştirme
git commit --amend -m "Yeni mesaj"

# Son commit'e dosya ekleme
git add <dosya>
git commit --amend --no-edit

# Commit'i geri alma (soft reset)
git reset --soft HEAD~1

# Commit'i geri alma (hard reset)
git reset --hard HEAD~1

# Belirli bir commit'e geri dönme
git reset --hard <commit-hash>
```

### Commit Geçmişi

```bash
# Commit geçmişini görme
git log

# Kısa format log
git log --oneline

# Grafik formatında log
git log --graph --pretty=oneline --abbrev-commit

# Belirli sayıda commit gösterme
git log -n 5

# Belirli dosyanın geçmişi
git log -- <dosya-adı>

# Commit'ler arası fark
git diff <commit1>..<commit2>
```

---

## 🔍 Geçmiş ve Log İşlemleri

### Detaylı Log Komutları

```bash
# Güzel formatlanmış log
git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short

# Son değişiklikleri gösterme
git show

# Belirli commit'in detayları
git show <commit-hash>

# Dosya değişiklik geçmişi
git blame <dosya-adı>

# Kimlerin ne zaman commit yaptığını görme
git shortlog -s -n
```

### Diff İşlemleri

```bash
# Working directory ile staging area farkı
git diff

# Staging area ile son commit farkı
git diff --staged

# İki commit arası fark
git diff <commit1> <commit2>

# İki branch arası fark
git diff <branch1>..<branch2>

# Sadece dosya isimlerini gösterme
git diff --name-only
```

### Arama İşlemleri

```bash
# Kod içinde arama
git grep "aranacak-metin"

# Commit mesajlarında arama
git log --grep="aranacak-metin"

# Yazar adına göre arama
git log --author="yazar-adı"

# Tarih aralığında arama
git log --since="2 weeks ago" --until="1 week ago"
```

---

## 🏷️ Tag İşlemleri

### Tag Oluşturma ve Yönetimi

```bash
# Lightweight tag oluşturma
git tag <tag-adı>

# Annotated tag oluşturma
git tag -a <tag-adı> -m "Tag açıklaması"

# Belirli commit'e tag ekleme
git tag -a <tag-adı> <commit-hash> -m "Açıklama"

# Tag'leri listeleme
git tag
git tag -l "v1.*"            # Pattern ile arama

# Tag detaylarını görme
git show <tag-adı>

# Tag'leri push etme
git push origin <tag-adı>
git push --tags              # Tüm tag'ler

# Tag silme
git tag -d <tag-adı>         # Local
git push origin :refs/tags/<tag-adı>  # Remote
```

---

## 🔧 Konfigürasyon

### Git Ayarları

```bash
# Global ayarlar
git config --global user.name "Adınız Soyadınız"
git config --global user.email "email@example.com"

# Editor ayarlama
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "vim"          # Vim

# Alias'lar oluşturma
git config --global alias.st "status"
git config --global alias.co "checkout"
git config --global alias.br "branch"
git config --global alias.ci "commit"

# Mevcut konfigürasyonu görme
git config --list
git config --global --list

# Belirli bir ayarı görme
git config user.name
```

### Faydalı Alias'lar

```bash
# Gelişmiş alias'lar
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git config --global alias.unstage "reset HEAD --"
git config --global alias.last "log -1 HEAD"
git config --global alias.visual "!gitk"
```

---

## ⚡ İleri Seviye Komutlar

### Stash İşlemleri

```bash
# Değişiklikleri geçici olarak saklama
git stash
git stash push -m "Açıklama"

# Belirli dosyaları stash'leme
git stash push <dosya-adı>

# Stash listesini görme
git stash list

# Stash'i uygulama
git stash pop               # Son stash'i uygula ve sil
git stash apply             # Son stash'i uygula ama silme

# Belirli stash'i uygulama
git stash apply stash@{2}

# Stash silme
git stash drop stash@{0}
git stash clear             # Tüm stash'leri silme
```

### Submodule İşlemleri

```bash
# Submodule ekleme
git submodule add <repository-url> <path>

# Submodule'leri güncelleme
git submodule update --init --recursive

# Submodule'leri en son versiyona çekme
git submodule update --remote

# Submodule silme
git submodule deinit <path>
git rm <path>
```

### Bisect (Binary Search)

```bash
# Bug arama başlatma
git bisect start

# İyi ve kötü commit'leri belirleme
git bisect bad              # Mevcut commit kötü
git bisect good <commit>    # Belirli commit iyi

# Otomatik test ile bisect
git bisect run <test-script>

# Bisect'i sonlandırma
git bisect reset
```

### Worktree

```bash
# Yeni worktree oluşturma
git worktree add <path> <branch>

# Worktree'leri listeleme
git worktree list

# Worktree silme
git worktree remove <path>
```

---

## 🛠️ Sorun Giderme

### Yaygın Problemler ve Çözümleri

```bash
# Yanlış commit mesajını düzeltme
git commit --amend -m "Doğru mesaj"

# Yanlış dosyayı commit'ten çıkarma
git reset HEAD~1
git add <doğru-dosyalar>
git commit -m "Düzeltilmiş commit"

# Merge conflict çözme
git status                  # Çakışan dosyaları görme
# Dosyaları manuel olarak düzenle
git add <dosya>
git commit

# Lost commit'leri bulma
git reflog
git cherry-pick <commit-hash>

# Dosyayı önceki haline döndürme
git checkout <commit-hash> -- <dosya-adı>
```

### Cleanup İşlemleri

```bash
# Untracked dosyaları silme
git clean -f                # Dosyaları sil
git clean -fd               # Dosya ve klasörleri sil
git clean -n                # Silinecekleri göster (dry run)

# Remote tracking branch'leri temizleme
git remote prune origin

# Garbage collection
git gc                      # Repository'yi optimize et
git gc --aggressive         # Agresif temizlik
```

---

## 📊 Git Workflow Örnekleri

### Feature Branch Workflow

```bash
# 1. Ana branch'ten yeni feature branch'i oluştur
git checkout main
git pull origin main
git checkout -b feature/yeni-ozellik

# 2. Geliştirme yap
git add .
git commit -m "Yeni özellik eklendi"

# 3. Remote'a push et
git push -u origin feature/yeni-ozellik

# 4. Pull request oluştur (GitHub/GitLab'da)
# 5. Review sonrası merge et
git checkout main
git pull origin main
git branch -d feature/yeni-ozellik
```

### Hotfix Workflow

```bash
# 1. Ana branch'ten hotfix branch'i oluştur
git checkout main
git checkout -b hotfix/kritik-bug

# 2. Bug'ı düzelt
git add .
git commit -m "Kritik bug düzeltmesi"

# 3. Ana branch'e merge et
git checkout main
git merge hotfix/kritik-bug
git push origin main

# 4. Hotfix branch'ini sil
git branch -d hotfix/kritik-bug
```

### Release Workflow

```bash
# 1. Release branch'i oluştur
git checkout develop
git checkout -b release/v1.0.0

# 2. Version numarasını güncelle
# package.json, version dosyaları vs.
git add .
git commit -m "Version 1.0.0 için hazırlık"

# 3. Ana branch'e merge et
git checkout main
git merge release/v1.0.0

# 4. Tag oluştur
git tag -a v1.0.0 -m "Version 1.0.0 release"
git push origin main --tags

# 5. Develop branch'e geri merge et
git checkout develop
git merge release/v1.0.0
git push origin develop

# 6. Release branch'ini sil
git branch -d release/v1.0.0
```

---

## 📚 Faydalı İpuçları

### Commit Mesajı Best Practices

```
feat: yeni özellik ekleme
fix: bug düzeltmesi
docs: dokümantasyon güncellemesi
style: kod formatı değişiklikleri
refactor: kod refactoring
test: test ekleme/düzenleme
chore: build process, dependency güncellemeleri
```

### Git Hooks Örnekleri

```bash
# Pre-commit hook (test çalıştırma)
#!/bin/sh
npm test
if [ $? -ne 0 ]; then
  echo "Tests failed, commit aborted"
  exit 1
fi
```

### Performance İpuçları

```bash
# Büyük dosyalar için
git config core.preloadindex true
git config core.fscache true
git config gc.auto 256

# Partial clone (büyük repository'ler için)
git clone --filter=blob:none <url>
```

---

## 🔗 Faydalı Kaynaklar

- [Git Official Documentation](https://git-scm.com/doc)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [Interactive Git Tutorial](https://learngitbranching.js.org/)

---

## 📝 Notlar

> **Dikkat:** `--force` parametresi kullanan komutlar tehlikeli olabilir. Kullanmadan önce durumu iyice analiz edin.

> **İpucu:** Komutları denemeden önce `--dry-run` parametresi ile test edebilirsiniz.

> **Öneriler:** Düzenli olarak `git status` komutu ile durumu kontrol edin.

---

<div align="center">

**🎯 Bu kılavuz sürekli güncellenmektedir. Katkılarınızı bekliyoruz!**

Made with ❤️ by developers, for developers

</div>
