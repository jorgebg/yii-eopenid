Last news
---------
Some time ago I developed this extension for [InDaHouseRulez SL](http://www.indahouserulez.com). I no longer work there, but I still support the extension.

The extension was released under the [MIT license](http://www.opensource.org/licenses/mit-license.php), so I made a fork on [GitHub](https://github.com), where you'll find the latest version:

[https://github.com/jorgebg/yii-eopenid](https://github.com/jorgebg/yii-eopenid)

Introduction
------------
EOpenID class extends from CBaseUserIdentity and implements the OpenID protocol to authenticate a user. Based on **Mewp's [LightOpenID](http://gitorious.org/lightopenid)** class.


###Resources
* [InDaHouseRulez SL](http://www.indahouserulez.com)
* [OpenID](http://openid.net/)
* [LightOpenID](http://gitorious.org/lightopenid)



##Documentation

###Requirements
* Yii 1.0 or above

###Installation
* Extract the release file under `protected/components`

###Usage
The action:

~~~
[php]

    public function actionOpenIDLogin() {
        $openid=new EOpenID;

        if(!isset($_GET['openid_mode'])) {
            if(isset($_POST['openid_identifier'])) {
                $openid->authenticate($_POST['openid_identifier']);
            }
        }
        elseif(isset($_GET['openid_mode'])) {
            $openid->validate();
            Yii::app()->user->login($openid);
        }

        $this->render('openIDLogin',array('openid'=>$openid));
    }

~~~


The view:

~~~
[php]

<div class="form">
<?php echo CHtml::beginForm(); ?>

	<div class="row">
		<?php echo CHtml::label('Identifier:', 'openid_identifier'); ?>
		<?php echo CHtml::textField('openid_identifier', '', array('size'=>40)); ?>
		<p class="hint">
			Hint: You may login with <tt>https://www.google.com/accounts/o8/id</tt>.
		</p>
	</div>

	<div class="row buttons">
		<?php echo CHtml::submitButton('Login'); ?>
	</div>

<?php echo CHtml::endForm(); ?>
</div><!-- form -->

~~~

##Change Log

###November 2, 2010
* Updated to new LightOpenID version 0.3 (thanks [hightman](http://www.yiiframework.com/forum/index.php?/topic/12727-eopenid-and-lightopenid-03/page__view__findpost__p__62429))

###July 27, 2010
* Initial release.

###July 28, 2010
* Renamed as EOpenID.
* PHP5 object constructor.
