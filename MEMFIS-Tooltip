/* ===========================================================
 * bootstrap-confirmation.js v1.0.1
 * http://ethaizone.github.io/Bootstrap-Confirmation/
 * ===========================================================
 * Copyright 2013 Nimit Suwannagate <ethaizone@hotmail.com>
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * =========================================================== */


!function ($) {

	"use strict"; // jshint ;_;


 /* CONFIRMATION PUBLIC CLASS DEFINITION
	* =============================== */

	//var for check event at body can have only one.
	var event_body = false;

	var Confirmation = function (element, options) {
		var that = this;

		// remove href attribute of button
		$(element).removeAttr('href')

		this.init('confirmation', element, options)

		$(element).on('show', function(e) {
			console.log("show event below:");       //Bill added for debug      Singleton 
			console.log(e);                         //Bill added for debug
			var options = that.options;
			var all = options.all_selector;
			if(options.singleton) {
				$(all).not(that.$element).confirmation('hide');
			}
		});

		$(element).on('shown', function(e) {
			console.log("shown event below:");      //Bill added for debug      Popout
			console.log(e);                         //Bill added for debug
			var options = that.options;
			var all = options.all_selector;
//			$(this).next('.popover').one('click.dismiss.confirmation', '[data-dismiss="confirmation"]', $.proxy(that.hide, that))
			console.log("shown > this")
			console.log(this)
			$(this).next('.popover').one('click.dismiss.confirmation', '[data-dismiss]', $.proxy(that.hide, that))    //Bill added for confirmation plug-in
			if(that.isPopout()) {
				if(!event_body) {
					event_body = $('body').on('click', function (e) {
						if($(all).is(e.target)) return;
						if($(all).has(e.target).length) return;
						if($(all).next('div').has(e.target).length) return;

						$(all).confirmation('hide');
						$('body').unbind(e);
						event_body = false;

						return;
					});
				}
			}
		});
	}


	/* NOTE: CONFIRMATION EXTENDS BOOTSTRAP-TOOLTIP.js
		 ========================================== */

	Confirmation.prototype = $.extend({}, $.fn.tooltip.Constructor.prototype, {

		constructor: Confirmation

		, setContent: function () {
				var $tip = this.tip()
//					, $btnOk = this.btnOk()
//					, $btnCancel = this.btnCancel()
				//Bill added for confirmation plug-in
					, $btnModify = this.btnModify()
					, $btnDelete = this.btnDelete()
					, $btnClose = this.btnClose()
					, title = this.getTitle()
					, href = this.getHref()
					, target = this.getTarget()
					, $e = this.$element
//					, btnOkClass = this.getBtnOkClass()
//					, btnCancelClass = this.getBtnCancelClass()
//					, btnOkLabel = this.getBtnOkLabel()
//					, btnCancelLabel = this.getBtnCancelLabel()
				//Bill added for confirmation plug-in
					, btnModifyClass = this.getBtnModifyClass()
					, btnDeleteClass = this.getBtnDeleteClass()
					, btnCloseClass = this.getBtnCloseClass()
					, btnModifyLabel = this.getBtnModifyLabel()
					, btnDeleteLabel = this.getBtnDeleteLabel()
					, btnCloseLabel = this.getBtnCloseLabel()
					, o = this.options
				console.log("tip()")        //Bill added for debug
				console.log($tip.get(0))           //Bill added for debug
				$tip.find('.popover-title').text(title)

//				$btnOk.addClass(btnOkClass).html(btnOkLabel).attr('href', href).attr('target', target).on('click', o.onConfirm)
//				$btnCancel.addClass(btnCancelClass).html(btnCancelLabel).on('click', o.onCancel)
				
				$btnModify.addClass(btnModifyClass).html(btnModifyLabel).attr('href', href).attr('target', target).on('click', o.onModify)
				$btnDelete.addClass(btnDeleteClass).html(btnDeleteLabel).attr('href', href).attr('target', target).on('click', o.onDelete)
				$btnClose.addClass(btnCloseClass).html(btnCloseLabel).attr('href', href).attr('target', target).on('click', o.onClose)
				
				$tip.removeClass('fade top bottom left right in')
			}

		, hasContent: function () {
				return this.getTitle()
			}

		, isPopout: function () {
				var popout
					, $e = this.$element
					, o = this.options

				popout = $e.attr('data-popout') || (typeof o.popout == 'function' ? o.popout.call($e[0]) :	o.popout)

				if(popout == 'false') popout = false;

				return popout
			}


		, getHref: function () {
				var href
					, $e = this.$element
					, o = this.options

				href = $e.attr('data-href') || (typeof o.href == 'function' ? o.href.call($e[0]) :	o.href)

				return href
			}

		, getTarget: function () {
				var target
					, $e = this.$element
					, o = this.options

				target = $e.attr('data-target') || (typeof o.target == 'function' ? o.target.call($e[0]) :	o.target)

				return target
			}

		, getBtnOkClass: function () {
				var btnOkClass
					, $e = this.$element
					, o = this.options

				btnOkClass = $e.attr('data-btnOkClass') || (typeof o.btnOkClass == 'function' ? o.btnOkClass.call($e[0]) :	o.btnOkClass)

				return btnOkClass
			}

		, getBtnCancelClass: function () {
				var btnCancelClass
					, $e = this.$element
					, o = this.options

				btnCancelClass = $e.attr('data-btnCancelClass') || (typeof o.btnCancelClass == 'function' ? o.btnCancelClass.call($e[0]) :	o.btnCancelClass)

				return btnCancelClass
			}
		
		//Bill added for confirmation plug-in;
		, getBtnModifyClass: function(){
				var btnModifyClass
					, $e = this.$element
					, o = this.options
				
				btnModifyClass = $e.attr('data-btnModifyClass') || (typeof o.btnModifyClass == 'function' ? o.btnModifyClass.call($e[0]) : o.btnModifyClass)
				
				return btnModifyClass
		}
			
		, getBtnDeleteClass: function(){
				var btnDeleteClass
					, $e = this.$element
					, o = this.options
		
				btnDeleteClass = $e.attr('data-btnDeleteClass') || (typeof o.btnDeleteClass == 'function' ? o.btnDeleteClass.call($e[0]) : o.btnDeleteClass)
				
				return btnDeleteClass
		}
			
		, getBtnCloseClass: function(){
				var btnCloseClass
					, $e = this.$element
					, o = this.options

				btnCloseClass = $e.attr('data-btnCloseClass') || (typeof o.btnCloseClass == 'function' ? o.btnCloseClass.call($e[0]) : o.btnCloseClass)
				
				return btnCloseClass
		}

		, getBtnOkLabel: function () {
				var btnOkLabel
					, $e = this.$element
					, o = this.options

				btnOkLabel = $e.attr('data-btnOkLabel') || (typeof o.btnOkLabel == 'function' ? o.btnOkLabel.call($e[0]) :	o.btnOkLabel)

				return btnOkLabel
			}

		, getBtnCancelLabel: function () {
				var btnCancelLabel
					, $e = this.$element
					, o = this.options

				btnCancelLabel = $e.attr('data-btnCancelLabel') || (typeof o.btnCancelLabel == 'function' ? o.btnCancelLabel.call($e[0]) :	o.btnCancelLabel)

				return btnCancelLabel
			}
		
		//Bill added for confirmation plug-in
		
		, getBtnModifyLabel: function () {
				var btnModifyLabel
					, $e = this.$element
					, o = this.options

				btnModifyLabel = $e.attr('data-btnModifyLabel') || (typeof o.btnModifyLabel == 'function' ? o.btnModifyLabel.call($e[0]) :	o.btnModifyLabel)

				return btnModifyLabel
			}
		
		, getBtnDeleteLabel: function () {
			var btnDeleteLabel
				, $e = this.$element
				, o = this.options

			btnDeleteLabel = $e.attr('data-btnDeleteLabel') || (typeof o.btnDeleteLabel == 'function' ? o.btnDeleteLabel.call($e[0]) :	o.btnDeleteLabel)

			return btnDeleteLabel
		}
		
		, getBtnCloseLabel: function () {
			var btnCloseLabel
				, $e = this.$element
				, o = this.options

			btnCloseLabel = $e.attr('data-btnCloseLabel') || (typeof o.btnCloseLabel == 'function' ? o.btnCloseLabel.call($e[0]) :	o.btnCloseLabel)

			return btnCloseLabel
		}

		, tip: function () {
				this.$tip = this.$tip || $(this.options.template)
				return this.$tip
			}

		, btnOk: function () {
				var $tip = this.tip()
				return $tip.find('.popover-content > div > a:not([data-dismiss="confirmation"])')
			}

		, btnCancel: function () {
				var $tip = this.tip()
				return $tip.find('.popover-content > div > a[data-dismiss="confirmation"]')
			}
		
		//Bill added for confirmation Plug-in
		
		, btnModify: function (){
				var $tip = this.tip()
				return $tip.find('.popover-content > div > a[data-dismiss="test_Modify"]')      //temp
			}
		
		, btnDelete: function (){
			var $tip = this.tip()
			return $tip.find('.popover-content > div > a[data-dismiss="test_Delete"]')          //temp
		}
		
		, btnClose: function (){
			var $tip = this.tip()
			return $tip.find('.popover-content > div > a[data-dismiss="test_Close"]')          //temp
		}

		, hide: function () {
				var $btnOk = this.btnOk()
					, $btnCancel = this.btnCancel()

				$.fn.tooltip.Constructor.prototype.hide.call(this)

				$btnOk.off('click')
				$btnCancel.off('click')

				return this
			}

		, destroy: function () {
				this.hide().$element.off('.' + this.type).removeData(this.type)
			}

        , setOptions: function (newOptions) {
                this.options = $.extend({}, this.options, newOptions || {});
			}

	})


 /* CONFIRMATION PLUGIN DEFINITION
	* ======================= */

	var old = $.fn.confirmation

	$.fn.confirmation = function (option, param) {
		var that = this
		return this.each(function () {
			var $this = $(this)
				, data = $this.data('confirmation')
				, options = typeof option == 'object' && option
			options = options || {}
			options.all_selector = that.selector
			console.log("confirmation options.all_selector")    //Bill added for debug
			console.log(options)    							//Bill added for debug
			if (!data) $this.data('confirmation', (data = new Confirmation(this, options)))
			if (typeof option == 'string') {
                if (option === 'option') {
                    data.setOptions(param)
                } else {
                    data[option]();
                }
            }
		})
	}

	$.fn.confirmation.Constructor = Confirmation

	$.fn.confirmation.defaults = $.extend({} , $.fn.tooltip.defaults, {
		placement: 'top'
		, trigger: 'click'
		, target : '_self'
		, href   : '#'
		, title: 'Pls choice:'
		, template: '<div class="popover" style="max-width: 300px">' +
				'<div class="arrow"></div>' +
				'<h3 class="popover-title"></h3>' +
				'<div class="popover-content text-center">' +
				'<div class="btn-group" >' +
				'<a class="btn btn-small" href="" target="" data-dismiss="test_Modify"></a>' +
				'<a class="btn btn-small" href="" target="" data-dismiss="test_Delete"></a>' +
				'<a class="btn btn-small" href="" target="" data-dismiss="test_Close"></a>' +
				'</div>' +
				'</div>' +
				'</div>'
//		, btnOkClass:  'btn-primary'
//		, btnCancelClass:  'btn-primary'
//		, btnOkLabel: '<span class="glyphicon glyphicon-edit" aria-hidden="true"></span> Modify'
//		, btnCancelLabel: '<span class="glyphicon glyphicon-trash" aria-hidden="true"></span> Delete'
		, btnModifyClass:  'btn-primary'
		, btnDeleteClass:  'btn-danger'
		, btnCloseClass:  'btn-warning'
		, btnModifyLabel:  '<span class="glyphicon glyphicon-edit" aria-hidden="true"></span> Modify'
		, btnDeleteLabel:  '<span class="glyphicon glyphicon-trash" aria-hidden="true"></span> Delete'
		, btnCloseLabel:  '<span class="glyphicon glyphicon-remove" aria-hidden="true"></span> Close'
		, singleton: false
		, popout: false
//		, onConfirm: function(){}
//		, onCancel: function(){}
		, onModify: function(){}
		, onDelete: function(){}
		, onClose: function(){}
	})


 /* POPOVER NO CONFLICT
	* =================== */

	$.fn.confirmation.noConflict = function () {
		$.fn.confirmation = old
		return this
	}

}(window.jQuery);
