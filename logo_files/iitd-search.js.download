$(function () {
	$('a[href="kksearch"]').on('click', function(event) {
		
		event.preventDefault();
		
		THEMEMASCOT.slider = {

			init: function() {

				var t = setTimeout(function() {
					THEMEMASCOT.slider.TM_typedAnimation();
				}, 0);

			},
			
			TM_typedAnimation: function() {
				var $typed_text_carousel = $('.typed-text-carousel');
				if ( $typed_text_carousel.length > 0 ) {
					$typed_text_carousel.each(function() {
						var string_1 = $(this).find('span:first-child').text();
						var string_2 = $(this).find('span:nth-child(2)').text();
						var string_3 = $(this).find('span:nth-child(3)').text();
						var str = '';
						var $this = $(this);
						if (!string_2.trim() || !string_3.trim()) {
							str = [string_1];
						}
						if (!string_3.trim() && string_2.length) {
							str = [string_1, string_2];
						}
						if (string_1.length && string_2.length && string_3.length) {
							str = [string_1, string_2, string_3];
						}
						var speed = $(this).data('speed');
						var back_delay = $(this).data('back_delay');
						var loop = $(this).data('loop');
						$(this).typed({
							strings: str,
							typeSpeed: speed,
							backSpeed: 0,
							backDelay: back_delay,
							cursorChar: "|",
							loop: loop,
							contentType: 'text',
							loopCount: false
						});
					});
				}
			}
		}
		THEMEMASCOT.slider.init();
		
		$('#search').addClass('open');
		
		setTimeout(function() { // To wait for the animation effect of 0.5 secs
			$('#wrapper').addClass('kk-blurbg');
			// $('#style-switcher').addClass('kk-blurbg');
		}, 500);

		$('#search').focus();
	});
	
	$('#kk-typed').on('click keyup', function(event) {
		// event.preventDefault();
		$('#kk-typed').addClass('dn');
		$('#kk-inp').removeClass('dn');
		$('#kk-inp').focus();
	});
	
	$('#search, #search button.close').on('click keyup', function(event) {
		// if (event.target == this || event.target.className == 'close' || event.keyCode == 27) {
						
		if (event.target.className == 'close' || event.target.className == 'fa fa-close' || event.keyCode == 27) {
			if($("#search").hasClass('open')) {
				$('#wrapper').removeClass('kk-blurbg');
				// $('#style-switcher').removeClass('kk-blurbg');
				$('#kk-typed').removeClass('dn');
				$('#kk-inp').addClass('dn');
				$('#kk-inp').val('');
				$('#search_results').html('');
				$('#search_results').removeClass('visible');
				$('#search').focus();
				$('#search').removeClass('open');
			}
		}
		if(event.keyCode != 27) {
			if((event.target.className == 'close' || event.target.className == 'fa fa-close') && event.button == 0) {
				if($("#search").hasClass('open')) {
					$('#wrapper').removeClass('kk-blurbg');
					// $('#style-switcher').removeClass('kk-blurbg');
					$('#kk-typed').removeClass('dn');
					$('#kk-inp').addClass('dn');
					$('#search').focus();
					$('#search').removeClass('open');
				}
			}
			else {
				if(event.keyCode == 9) {
					event.preventDefault();
					event.stopPropagation();
				}
				$('#kk-typed').addClass('dn');
				$('#kk-inp').removeClass('dn');
				$('#kk-inp').focus();
				if($('#kk-inp').val() == '') {
					if((event.keyCode >= 48 && event.keyCode < 62) || (event.keyCode >= 65 && event.keyCode < 91) || (event.keyCode >= 96 && event.keyCode < 106)) {
						var lc = String.fromCharCode(event.keyCode).toLowerCase();
						$('#kk-inp').val(lc);
						showResult();
					}
				}
			}
		}
	});
});


function showResult(str) {
	var search_in = $('input[name=radio]:checked', '#iitd-search').val().trim();
	var search_term = $('#kk-inp').val().trim();
	if (search_term == '') {
		$('#search_results').html('');
		$('#search_results').removeClass('visible');
	}
	else {
		$.ajax({
			url: 'includes/search.php',
			type: 'post',
			data: {
				q: search_term, s_in: search_in
			},
			dataType: 'json',
			success: function(returnData){
				//Blank the search_results div.
				$('#search_results').html('');
				$('#search_results').addClass('visible');
				$('#search_results').append('<h4 class="text-white"><i class="fa fa-info-circle"></i> Pages/Information for you:</h4>');
				//Parse the result that we got back from search.php
				// var results = JSON.parse(returnData);
				//Loop through the results array and append it to
				//the search_results div.
				// $.each(returnData, function(key, value){
					// $('#search_results').append('<div><a href="'+key+'">'+value+'</a></div>');
				// });
				// alert(returnData.length);
				
				for(var i in returnData) {
					// var res_arr = returnData[i];
					for(var j in returnData[i]) {
						$('#search_results').append('<div><a target="_blank" href="'+returnData[i][j]+'">'+Object.keys(returnData[i])+'<i class="fa fa-external-link ml-5 va-m"></i></a></div>');
					}
				}
				
				//If the results array is empty, display a
				//message saying that no results were found.
				if(returnData.length == 0){
					$('#search_results').html('No results found!');
				}
				
				// $("#search_results :nth-child(2)").addClass( "s-selected" );
				// var $input = $('#kk-inp'),
				// current_index = $('.selected').index(),
				// $number_list = $('#search_results'),
				// $options = $number_list.find('div'),
				// items_total = $options.length;
				
				
				// $input.bind('keyup', function(e) {
					// e.preventDefault();
					// if (e.keyCode == 40) {
						// if (current_index + 1 < items_total) {
							// current_index++;
							// change_selection();
						// }
					// } else if (e.keyCode == 38) {
						// if (current_index > 0) {
							// current_index--;
							// change_selection();
						// }
					// }
				// });

				// function change_selection() {
					// $options.removeClass('s-selected');
					// $options.eq(current_index).addClass('s-selected');
					// $input.val(current_index);
				// }​
				
				
				// Make the first search result selected by default and enabling keyboard selection

					// if ($("div").parents("#search_results").length == 1) {

						// var $input = $('#kk-inp'),
						// current_index = $('.selected').index(),
						// $number_list = $('#search_results'),
						// $options = $number_list.find('div'),
						// items_total = $options.length;

						// $input.val(current_index);

						// $input.bind('keyup', function(event) {
							// event.preventDefault();
							// if (event.keyCode == 40) {
								// if (current_index + 1 < items_total) {
									// current_index++;
									// change_selection();
								// }
							// } else if (event.keyCode == 38) {
								// if (current_index > 0) {
									// current_index--;
									// change_selection();
								// }
							// }
						// });

						// function change_selection() {
							// event.preventDefault();
							// $options.removeClass('selected');
							// $options.eq(current_index).addClass('selected');
							// $input.val(current_index);
						// }​

					// }
					// else {

					// }

				// Make the first search result selected by default and enabling keyboard selection
		
			}
		});
	}
}