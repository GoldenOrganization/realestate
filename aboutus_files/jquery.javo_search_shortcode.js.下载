( function( $ ) {

	var jv_search1_shortcode = function( id ){
		this.el			= $( id );
		this.initialize();
	}

	jv_search1_shortcode.prototype = {
		constructor	: jv_search1_shortcode,

		initialize : function()
		{
			var
				obj			= this,
				elSelectize	= $( '[data-selectize]', obj.el );

			elSelectize.length && typeof $.fn.selectize == 'function' && obj.bindSelectize( elSelectize );

			obj
				.setupGooglePlaceField()
				.amenitiesOpener()
				.setPriceField();

			$( document )
				.on( 'click', obj.el.find( '.jv-search1-form-opener' ).selector, obj.toggleForm() )
				.on( 'click', obj.el.find( '.jv-search1-morefilter-opener' ).selector, obj.toggleMoreFilter() )
				.on( 'click', obj.el.find( '.javo-geoloc-trigger' ).selector, obj.GeoLocation() );
		},

		setupGooglePlaceField : function() {

			var element		= $( "[name='radius_key']", this.el )[0];

			if( typeof element != 'undefined' ) {
				new google.maps.places.Autocomplete( element );
			}

			return this;

		},

		toggleForm : function() {
			var obj				= this;
			return function( e ){
				e.preventDefault();
				var
					container	= $( this ).closest( '.javo-shortcode' )
					, form		= $( "form", container );

				if( container.hasClass( 'active' ) ) {
					form.slideUp( function() {
						container.removeClass( 'active' );
					} );

				}else{
					container.addClass( 'active' );
					form.slideDown();
				}
			}
		},

		toggleMoreFilter : function() {
			var obj				= this;

			return function (e)
			{
				e.preventDefault();

				var
					container		= $( this ).closest( '.javo-shortcode' )
					, morePanel	= $( '.jv-search1-morefilter-row', container );

				if( container.hasClass( 'more-open' ) ) 	{

					morePanel.slideUp( function() {
						container.removeClass( 'more-open' );
					});

				}else{
					container.addClass( 'more-open' );
					morePanel.slideDown();
				}
			}
		},

		GeoLocation : function() {
			return function( e ) {
				e.preventDefault();
				var
					form		= $( this ).closest( 'form' );

				$( this ).addClass( 'fa-spin' );

				$( "<input>" )
					.attr({
						name	: 'geolocation',
						type		: 'hidden',
						value		: '1'
				}).appendTo( form );

				form.submit();

			}
		},

		bindSelectize : function( elements ){
			elements.each( function( idx, element ){
				var objInstance = $( this ).selectize();
			} );
			return true;
		},

		setPriceField : function() {

			var
				obj				= this
				, el				= obj.el
				, element		= $( "div.javo-price-slider", el )
				, container	= element.parent()
				, minPrice		=  parseInt( $( "[name='minPrice']", container ).val() || 0 )
				, maxPrice	=  parseInt( $( "[name='maxPrice']", container ).val() || 100 )
				, option			= {
					start			: [ minPrice, maxPrice ]
					, connect	: true
					, range		: { min :  minPrice, max : maxPrice }
				}

			if( !$.fn.noUiSlider || !element.length )
				return this;

			option.serialization	=	{
				lower :[
					$.Link( {
							target : $( "[name='minPrice']", container )
					}),
					$.Link( {
						target : $( '[data-min]', container )
						, method : function(v) {
							$( this ).html( '<span>' + v + '</span>' );
						}
						, format : {
							decimals	: 0
							, thousand	:','
						}
					})
				]
				, upper :[
					$.Link( {
							target : $( "[name='maxPrice']", container )
					}),
					$.Link({
						target : $( '[data-max]', container )
						, method : function(v) {
							$( this ).html( '<span>' + v + '</span>' );
						}
						, format : {
							decimals	: 0
							, thousand	:','
						}
					})
				]
			}

			element.noUiSlider( option );

			return this;
		},

		amenitiesOpener : function() {

			var obj = this;

			$( document ).on(
				'click',
				obj.el.find( '.bottom-amenities-opener-button' ).selector,
				function( e ){
					e.preventDefault();
					obj.el.toggleClass( 'advance-collapse' );
				}
			);
			return this;
		}
	};
	$.jvfrm_home_search_shortcode = function( id ) {
		new jv_search1_shortcode( id );
	}
} )( jQuery );