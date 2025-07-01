---
title: Devise Nedir Ve Devise Nasıl Kullanılır?
date: 2024-09-03 11:00:00 +0300
categories: [RubyonRails, Devise]
tags: [Devise]
description: Bu yazının içeriğinde devise notlarım ve devise kullanıma ait bilgiler olacaktır.    
---

# Devise Nedir?

Devise, Ruby on Rails uygulamaları için geliştirilmiş bir kimlik doğrulama (authentication) ve kullanıcı yönetimi çözümüdür. Kullanıcı oturumları, kayıtlar, şifre kurtarma, kullanıcı rolü gibi işlemleri kolayca gerçekleştirmek için birçok hazır fonksiyona sahiptir. Kısacası, Rails projelerinde hızlı ve güvenli bir kimlik doğrulama sistemi kurmanıza yardımcı olur ve genellikle kullanıcı yönetimi gerektiren projelerde yaygın olarak kullanılır.

# Devise Nasıl Kullanılır?

## 1. Devise Gem'ini Kurmak

Projemizde devise kullanmak için öncelikle `Gemfile` dosyasına aşağıdaki satırı eklememiz gerekir:

```ruby
gem 'devise'
```

Daha sonra terminalde aşağıdaki komut çalıştırılarak gem yüklenir:

```bash
bundle install
```

## 2. Devise Kurulumu

Devise’ı projeye dahil etmek için aşağıdaki komutu çalıştırın:

```bash
rails generate devise:install
```

Bu komut ile aşağıdaki işlemler yapılır:

- Devise için gerekli konfigürasyon dosyaları oluşturulur.
- `config/environments/development.rb` içine aşağıdaki satırın eklenmesi önerilir:

```ruby
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

- Flash mesajlarının (notice ve alert) gösterilebilmesi için layout dosyanıza şu kodlar eklenmelidir:

```erb
<p class="notice"><%= notice %></p>
<p class="alert"><%= alert %></p>
```

- Uygulamanın root path’i tanımlı olmalıdır, örneğin:

```ruby
root to: "home#index"
```

## 3. Kullanıcı Modeli Oluşturmak

Devise ile kullanıcı yönetimi için bir model oluşturmak gerekir. Örneğin `User` modeli için:

```bash
rails generate devise User
```

Bu komut `users` tablosunu ve kullanıcı kimlik doğrulama alanlarını içeren bir migration dosyası oluşturur. Daha sonra bu değişiklikleri veritabanına uygulamak için:

```bash
rails db:migrate
```

## 4. Devise Modülleri

Devise, kullanıcı modeline birçok modül entegre eder. Örnek olarak:

```ruby
devise :database_authenticatable, :registerable,
       :recoverable, :rememberable, :validatable
```

### Bu modüllerin anlamı:

- `:database_authenticatable`: E-posta ve şifre ile kimlik doğrulama sağlar.
- `:registerable`: Kullanıcının kayıt olmasına olanak tanır.
- `:recoverable`: Şifre sıfırlama işlemlerini yönetir.
- `:rememberable`: "Beni hatırla" özelliğini sağlar.
- `:validatable`: Şifre doğrulama (uzunluk, format vs.) kurallarını uygular.

İhtiyaca göre daha fazla modül (örneğin `:confirmable`, `:lockable`, `:timeoutable`) de eklenebilir.

## 5. Route Ayarları

Devise gerekli rotaları otomatik olarak tanımlar. `config/routes.rb` dosyasına şu satır eklenmelidir:

```ruby
devise_for :users
```

## 6. View (Görünüm) Dosyaları Oluşturmak

Varsayılan Devise sayfalarını özelleştirmek için view dosyaları oluşturabiliriz:

```bash
rails generate devise:views
```

Bu komut ile `app/views/devise/` klasörü altında kayıt, giriş, şifre kurtarma gibi sayfalar oluşur. Tasarımı özelleştirmek için bu dosyalar düzenlenebilir.

## 7. Oturum Kontrolü

Bazı controller veya action’ların sadece giriş yapmış kullanıcılar tarafından erişilmesini istiyorsanız:

```ruby
before_action :authenticate_user!
```

işlemi ilgili controller’a eklenmelidir.

## 8. Örnek Kullanım

Basit bir örnek ile, giriş yapmış kullanıcıya özel bir dashboard sayfası yapmak istiyorsak:

```ruby
# app/controllers/dashboard_controller.rb
class DashboardController < ApplicationController
  before_action :authenticate_user!
  def index
    # dashboard içeriği
  end
end
```

```ruby
# config/routes.rb
get 'dashboard', to: 'dashboard#index'
```

## 9. Ek Özellikler

Devise çok sayıda gelişmiş özelliği de destekler:

- **Confirmable:** E-posta ile kullanıcı doğrulaması
- **Lockable:** Hatalı giriş denemelerinde hesabı kilitleme
- **Timeoutable:** Belirli bir süre etkinlik olmazsa oturumu sonlandırma
- **Trackable:** Kullanıcının giriş tarihlerini ve IP adreslerini izleme

Bu modülleri kullanmak için modelde tanımlanmalı ve ilgili migrasyonlar eklenmelidir.

---

Devise, Rails uygulamanızda kullanıcı yönetimini hızlı, güvenli ve esnek bir şekilde çözmenizi sağlar. Özelleştirilebilir yapısı sayesinde küçük projelerden büyük sistemlere kadar yaygın bir çözümdür. Kullanımı oldukça kolaydır ve Rails topluluğu tarafından da geniş destek görmektedir.
