# README

## Rack
https://railsguides.jp/rails_on_rack.html

### overview
- APサーバーとフレームワークの中間に存在するもの
- Rackのおかげで両者が疎結合になり、組み合わせやすくなった
- Rackミドルウェア: Rack層からフレームワーク層の間で独自の処理を挟める


```ruby
def call(env)
  [http_status, http_headers, response_body]
end
```
- useメソッドでミドルウェアを追加できる
  - https://github.com/rack/rack-contrib

### RailsでもRackミドルウェアを利用している

```shell
% bin/rails middleware                                                                       ✔ │ 2.6.6 

use ActionDispatch::HostAuthorization
use Rack::Sendfile
use ActionDispatch::Static
use ActionDispatch::Executor
use ActiveSupport::Cache::Strategy::LocalCache::Middleware
use Rack::Runtime
use Rack::MethodOverride
use ActionDispatch::RequestId
use ActionDispatch::RemoteIp
use Sprockets::Rails::QuietAssets
use Rails::Rack::Logger
use ActionDispatch::ShowExceptions
use WebConsole::Middleware
use ActionDispatch::DebugExceptions
use ActionDispatch::ActionableExceptions
use ActionDispatch::Reloader
use ActionDispatch::Callbacks
use ActiveRecord::Migration::CheckPending
use ActionDispatch::Cookies
use ActionDispatch::Session::CookieStore
use ActionDispatch::Flash
use ActionDispatch::ContentSecurityPolicy::Middleware
use Rack::Head
use Rack::ConditionalGet
use Rack::ETag
use Rack::TempfileReaper
run RailsRackSample::Application.routes


# config.ruでは明示されてない
# 開発専用のものも含まれているためproduction環境では少し異なる
```

### Rackミドルウェアの実行順を指定できる
- config.middleware.use
- config.middleware.insert_after
- config.middleware.insert_before
- config.middleware.delete

### igaigaさんRailsの練習帳
https://zenn.dev/igaiga/books/rails-practice-note/viewer/rack_middleware_and_rack

