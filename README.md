##Smart editor rails gem

NHN에서 개발한 smart editor 를 레일즈 사용자들이 사용하기 쉽도록 만든 gem입니다.

rails3 이상에서 작동하도록 되어 있습니다.

Gemfile에 다음과 같이 추가해 주시고

    gem 'smart_editor'
    

bundle을 입력하여 gem을 설치한 다음에 

다음과 같은 커맨드를 입력하시면 부수적인 파일들이 설치됩니다.

    rails g smart_editor


application.js 에도 다음과 같이 추가해시면 됩니다.

    //= require smart_editor


그리고 form을 작성하실 때 text_area에 "smart-editor-text-area"라고 클래스를 주시면 됩니다. 

    <%= f.text_area :desc, :class => "smart-editor-text-area" %>
    

###이미지 업로드 기능 사용

혹시 이미지업로드 기능을 원하시면다면 다음과 같이 하시면 됩니다.

model에서 다음을 추가해 주시고

    has_editor_images
    
ex)

    class Post < ActiveRecord::Base
      has_editor_images
    end
    
    
controller 에서 다음을

    SmartEditor::bind_editor_images(self, "model name", [:create, :update])
    

여기서 두번쨰 파라메터인 model name  스마트 에디터의 편집기능이 적용될 모델의 이름을 적어주시면 됩니다.
세번째 파라메터인 [:create, :update]  스마트 에디터에서 편집된 내용이 적용되는 action들을 array로 적어주시면 됩니다.

ex)

    class PostsController < ApplicationController
      SmartEditor::bind_editor_images(self, "post", [:create, :update])
      
      def index
        ...
      end
      
      def create
        ...
      end 
      
      def update
        ...
      end
    end


view 에서는 form_for  안의 block 안에 

    <%= f.editor_image_field %>
    
을 입력해주시면 됩니다.

ex)

    <%= form_for(@post) do |f| %>
    
      <%= f.editor_image_field %>
      <%= f.text_area :desc, :class => "smart-editor-text-area" %>
    <% end %>
