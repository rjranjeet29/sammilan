<?php
ob_start();
session_start();
include 'api/db_config.php';
?>
<!DOCTYPE html>
<html lang="en">
<head>

		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
		<meta http-equiv="x-ua-compatible" content="ie=edge">

		<title>Sammilan</title>
		<link rel="shortcut icon" href="assets/images/favicon.png">

		<!-- fraimwork - css include -->
		<link rel="stylesheet" type="text/css" href="assets/css/bootstrap.min.css">

		<!-- icon css include -->
		<link rel="stylesheet" type="text/css" href="assets/css/fontawesome-all.css">
		<link rel="stylesheet" type="text/css" href="assets/css/flaticon.css">

		<!-- carousel css include -->
		<link rel="stylesheet" type="text/css" href="assets/css/slick.css">
		<link rel="stylesheet" type="text/css" href="assets/css/slick-theme.css">
		<link rel="stylesheet" type="text/css" href="assets/css/animate.css">
		<link rel="stylesheet" type="text/css" href="assets/css/owl.carousel.min.css">
		<link rel="stylesheet" type="text/css" href="assets/css/owl.theme.default.min.css">

		<!-- others css include -->
		<link rel="stylesheet" type="text/css" href="assets/css/magnific-popup.css">
		<link rel="stylesheet" type="text/css" href="assets/css/jquery.mCustomScrollbar.min.css">
		<link rel="stylesheet" type="text/css" href="assets/css/calendar.css">
		<link rel="stylesheet" type="text/css" href="assets/css/lightcase.css">

		<!-- color switcher css include -->
		<link rel="stylesheet" type="text/css" href="assets/css/colors/style-switcher.css">
		<link id="color_theme" rel="stylesheet" type="text/css" href="assets/css/colors/default.css">

		<!-- custom css include -->
		<link rel="stylesheet" type="text/css" href="assets/css/style.css">

	</head>


	<body>




		
		<!-- backtotop - start -->
		<div id="thetop" class="thetop"></div>
		<div class='backtotop'>
 			<a href="#thetop" class='scroll'>
				<i class="fas fa-angle-double-up"></i>
			</a>
		</div>
		<!-- backtotop - end -->

		<!-- preloader - start -->
		<div id="preloader2"></div>
		<!-- preloader - end -->





		<!-- header-section - start
		================================================== -->
		<header id="header-section" class="header-section sticky-header-section not-stuck clearfix">
			<!-- header-bottom - start -->
			<div class="header-bottom">
				<div class="container">
					<div class="row">
						<?php include"includes/header-index.php"?>
					</div>
				</div>
			</div>
			<!-- header-bottom - end -->
		</header>
		<!-- header-section - end
		================================================== -->





		<!-- altranative-header - start
		================================================== -->
			<?php include"includes/header-mobile.php";?>
		<!-- altranative-header - end
		================================================== -->





		<!-- slide-section - start
		================================================== -->
		<section id="slide-section" class="slide-section clearfix">
			<div id="main-carousel1" class="main-carousel1 owl-carousel owl-theme">
				<?php
				$queryslider = "SELECT * FROM `cj_slider` where status='1' order by order_no";
				$run_queryslider = mysqli_query($db, $queryslider);
				while($rowsldr = mysqli_fetch_array($run_queryslider))
				{
					$title = $rowsldr['title'];
					$slider_desc= $rowsldr['slider_desc'];
					$url = $rowsldr['url'];
					$image = $rowsldr['image'];
					?>
					<div class="item" style="background-image: url(webimages/sliderimage/<?=$image?>);">
						<div class="overlay-black">
							<div class="container">
								<div class="slider-item-content">

									<span class="medium-text">one stop</span>
									<h1 class="big-text"><?php echo $title; ?></h1>
									<small class="small-text"><?php echo $slider_desc; ?></small>

									<div class="link-groups">
										<a href="<?php echo $url; ?>" class="about-btn custom-btn">Read More</a>
										<!--a href="#!" class="start-btn">get started!</a-->
									</div>

								</div>
							</div>
						</div>
					</div>
					<?php		
				}
				?>

			</div>
		</section>
		<!-- slide-section - end
		================================================== -->





		<!-- upcomming-event-section - start
		================================================== -->
		<section id="upcomming-event-section" class="upcomming-event-section sec-ptb-100 clearfix">
			<div class="container">

				<!-- section-title - start -->
				<div class="section-title text-center mb-50">
					<small class="sub-title">upcomming events</small>
					<h2 class="big-title">Latest <strong>Awesome Events</strong></h2>
				</div>
				<!-- section-title - end -->

				<!-- upcomming-event-carousel - start -->
				<div id="upcomming-event-carousel" class="upcomming-event-carousel owl-carousel owl-theme">
					<?php
					$i=1;
					$sqllevent=mysqli_query($db, "Select * from cj_event inner join cj_event_category on cj_event.e_cat=cj_event_category.id where e_post_role like '%".@$_REQUEST["search"]."%' && cj_event.e_status='1'  && cj_event.latest_event='1' order by cj_event.mod_date DESC") or die(mysqli_error($db));
					while($levent=mysqli_fetch_assoc($sqllevent))
					{	?>
						<!-- item - start -->
						<div class="item">
							<div class="event-item">

								<div class="countdown-timer">
									<ul class="countdown-list" data-countdown="<?=date("Y/m/d",strtotime($levent['e_date']));?>"></ul>
								</div>

								<div class="event-image">
									<img src="webimages/event/<?=$levent['e_image'];?>" onError="this.src='webimages/imgerror.jpg'" alt="<?=$levent['e_title'];?>">
									<div class="post-date">
										<span class="date"><?=date("d",strtotime($levent['e_date']));?></span>
										<small class="month"><?=date("M",strtotime($levent['e_date']));?></small>
									</div>
								</div>

								<div class="event-content">
									<div class="event-title mb-30">
										<h3 class="title">
											<?=$levent['e_title'];?>
										</h3>
										<span class="ticket-price yellow-color">Tickets from ₹ <?=$levent['e_t_price'];?></span>
									</div>
									<div class="event-post-meta ul-li-block mb-30">
										<ul>
											<li>
												<span class="icon">
													<i class="far fa-clock"></i>
												</span>
												Start <?php echo date("h:i A",strtotime($levent['e_time_from']));?> - <?php echo date("h:i A",strtotime($levent['e_time_to']));?>
											</li>
											<li>
												<span class="icon">
													<i class="fas fa-map-marker-alt"></i>
												</span>
												<?=$levent['e_location'];?>
											</li>
										</ul>
									</div>
									<a href="event-details.php?e_id=<?=$levent['e_id'];?>" class="custom-btn">
										details
									</a>
								</div>

							</div>
						</div>
						<!-- item - end -->
						<?php
						$i++;
					}?>


				</div>
				<!-- upcomming-event-carousel - end -->

			</div>
		</section>
		<!-- upcomming-event-section - end
		================================================== -->





		<!-- about-section - start
		================================================== -->
		<section id="about-section" class="about-section sec-ptb-100 clearfix">
			<div class="container">
				<div class="row">

					<!-- section-title - start -->
					<div class="col-lg-4 col-md-12 col-sm-12">
						<div class="section-title text-left mb-30">
							<span class="line-style"></span>
							<small class="sub-title">we are Sammilan</small>
							<h2 class="big-title"><strong>No.1</strong> Events Management</h2>
							<!--p class="black-color mb-50">
								Lorem ipsum dollor site amet the best  consectuer adipiscing elites sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat insignia the consectuer adipiscing elit. 
							</p-->
							<a href="about.php?id=2" class="custom-btn">
								about sammilan
							</a>
						</div>
					</div>
					<!-- section-title - end -->

					<!-- about-item-wrapper - start -->
					<div class="col-lg-8 col-md-12 col-sm-12">
						<div class="section-title text-left mb-30">
							<small class="sub-title">Event Category</small>
						</div>
						<div class="about-item-wrapper ul-li">
							<ul>

								<?php
								$query = "SELECT * FROM `cj_event_category`";
								$run_query = mysqli_query($db, $query);
								while($rowcategory = mysqli_fetch_array($run_query))
								{
								?>
								<li>
									<a href="#!" class="about-item">
										<span class="icon">
											<img src="webimages/eventcategory/<?php echo $rowcategory['image']; ?>" height="40" width="40" onerror="this.src='../webimages/no-image.jpg'">
											<!--i class="flaticon-handshake"></i-->
										</span>
										<strong class="title"><?=$rowcategory['ev_category']?></strong>
										<!--small class="sub-title">More than 200 teams</small-->
									</a>
								</li>
								<?php
								}?>

							</ul>
						</div>
					</div>
					<!-- about-item-wrapper - end -->
					
				</div>
			</div>
		</section>
		<!-- about-section - end
		================================================== -->





		<!-- conference-section - start
		================================================== -->
		<section id="conference-section" class="conference-section clearfix">
			<div class="jarallax" style="background-image: url(assets/images/conference/pexels-photo-262669.jpg);">
				<div class="overlay-black sec-ptb-100">

					<div class="mb-50">
						<div class="container">
							<div class="row">

								<!-- section-title - start -->
								<div class="col-lg-6 col-md-12 col-sm-12">
									<div class="section-title text-left">
										<span class="line-style"></span>
										<small class="sub-title">Sammilan venues</small>
										<h2 class="big-title">Conference <strong>Rooms &amp; Hotels</strong></h2>
									</div>
								</div>
								<!-- section-title - end -->

								<!-- conference-location - start -->
								<div class="col-lg-6 col-md-12 col-sm-12">
									<div class="conference-location ul-li clearfix">
										<ul>

											<!-- country-select - start ->
											<li class="country-select">
												<form action="#!">
													<label for="country">Country :</label>
													<select class="custom-select" id="country">
														<option selected>Netherland</option>
														<option value="1">USA</option>
														<option value="2">england</option>
														<option value="3">germany</option>
													</select>	
												</form>
											</li>
											<!-- country-select - end -->

											<!-- city-select - start -->
											<li class="city-select">
												<form action="place.php">
													<label for="city">city :</label>
													<select class="custom-select" name="city" id="city" required onchange="this.form.submit()">
														<option value="">Select City</option>
														<?php
														$placeres=mysqli_query($db, "Select e_city from cj_place  where e_status='1' order by e_city") or die(mysqli_error($db));
														while($placeresfet=mysqli_fetch_assoc($placeres))
														{?><option value="<?=$placeresfet["e_city"]?>"><?=$placeresfet["e_city"]?></option><?php } ?>
													</select>	
												</form>
											</li>
											<!-- city-select - end -->

										</ul>
									</div>
								</div>
								<!-- conference-location - end -->

							</div>
						</div>
					</div>

					<!-- conference-content-wrapper - start -->
					<div class="tab-wrapper">

						<!-- tab-menu - start -->
						<div class="container">
							<div class="row justify-content-lg-start">
								<div class="col-lg-6 col-md-12 col-sm-12">
									<div class="tab-menu">
										<ul class="nav tab-nav mb-50">

											<?php
											$pi=1;
											$placeres=mysqli_query($db, "Select * from cj_place  where home_listing = '1' && e_status='1' order by mod_date DESC") or die(mysqli_error($db));
											while($placeresfet=mysqli_fetch_assoc($placeres))
											{?>
											<li class="nav-item">
												<a class="nav-link <?=(($pi==1)?'active':'')?>" id="nav-one-tab" data-toggle="tab" href="#nav-one<?=$pi?>" aria-expanded="true">
													<span class="image">
														<img src="webimages/place/<?=$placeresfet['e_image'];?>" alt="<?=$placeresfet['e_title'];?>" onError="this.src='../webimages/imgerror.jpg'">
													</span>
													<span class="title">
														<strong class="yellow-color"><?=$placeresfet['e_star']?> <i class="fas fa-star"></i>  </strong>
														<?=$placeresfet['e_title']?>
													</span>
													<small class="sub-title">Party Room <?=$placeresfet['e_hall']?></small>
													<small class="price yellow-color">Price from Rs <?=$placeresfet['e_hall_charge']?>/hall</small>
												</a>
											</li>
											<?php
											$pi++;
											}?>

										</ul>
										<div class="more-btn">
											<a href="place.php">
												<strong class="yellow-color">VIEW ALL</strong> HOTEL & RESORT
											</a>
										</div>
									</div>
								</div>
							</div>
						</div>
						<!-- tab-menu - end -->

						<!-- tab-content - start -->
						<div class="tab-content">
							<?php
							$dpi=1;
							$placeres=mysqli_query($db, "Select * from cj_place  where home_listing = '1' && e_status='1' order by mod_date DESC") or die(mysqli_error($db));
							while($placeresfet=mysqli_fetch_assoc($placeres))
							{?>
							<!-- tab-pane - start -->
							<div class="tab-pane fade <?=(($dpi==1)?'active show':'')?>" id="nav-one<?=$dpi?>" role="tabpanel" aria-labelledby="nav-one-tab" aria-expanded="true">
								<div class="image">
									<img src="webimages/place/<?=$placeresfet['e_image'];?>" alt="<?=$placeresfet['e_title'];?>" onError="this.src='webimages/imgerror.jpg'" style="width:100%; 
									margin-right:20px;">
									<a href="place-detail" class="custom-btn">
										Detail
									</a>
									<div class="badge-item">
										<div class="content">
											<i class="fas fa-star"></i>
											<strong><?=$placeresfet['e_star']?>.0</strong>
											<small>featured Place</small>
										</div>
									</div>
								</div>
							</div>
							<!-- tab-pane - end -->
							<?php
							$dpi++;
							}?>


						</div>
						<!-- tab-content - end -->

					</div>
					<!-- conference-content-wrapper - end -->

				</div>
			</div>
		</section>
		<!-- conference-section - end
		================================================== -->










		<!-- event-section - start
		================================================== -->
		<section id="event-section" class="event-section sec-ptb-100 bg-gray-light clearfix">
			<div class="container">

				<div class="mb-50">
					<div class="row">

						<!-- section-title - start -->
						<div class="col-lg-3 col-md-12 col-sm-12">
							<div class="section-title text-left">
								<span class="line-style"></span>
								<small class="sub-title">Sammilan events</small>
								<h2 class="big-title"><strong>event</strong> listing</h2>
							</div>
						</div>
						<!-- section-title - end -->

						<!-- event-tab-menu - start ->
						<div class="col-lg-8 col-md-12 col-sm-12">
							<div class="event-tab-menu clearfix">
								<ul class="nav">
									<li>
										<a class="active" data-toggle="tab" href="#conference-event">
											<strong><i class="fas fa-microphone"></i> conference</strong> event
										</a>
									</li>
									<li>
										<a data-toggle="tab" href="#playground-event">
											<strong><i class="fas fa-birthday-cake"></i> play ground</strong> event
										</a>
									</li>
									<li>
										<a class="active" data-toggle="tab" href="#musical-event">
											<strong><i class="fas fa-music"></i> musical</strong> event
										</a>
									</li>
									<li>
										<a data-toggle="tab" href="#other-event">
											<strong><i class="far fa-check-square"></i> other</strong> event
										</a>
									</li>
								</ul>
							</div>
						</div>
						<!-- event-tab-menu - end -->

					</div>
				</div>

				<!-- tab-content - start -->
				<div class="tab-content">

					<!-- conference-event - start -->
					<div id="conference-event" class="tab-pane fade in active show">
						<div class="row">

							<?php
							$i=1;
							$sql_ev=mysqli_query($db, "Select * from cj_event inner join cj_event_category on cj_event.e_cat=cj_event_category.id where e_post_role like '%".@$_REQUEST["search"]."%' && cj_event.e_status='1'  && cj_event.home_listing='1' order by cj_event.mod_date DESC limit 6") or die(mysqli_error($db));
							while($evrow=mysqli_fetch_assoc($sql_ev))
							{	?>
								<!-- event-item - start -->
								<div class="col-lg-6 col-md-12 col-sm-12">
									<div class="event-item clearfix">

										<!-- event-image - start -->
										<div class="event-image">
											<div class="post-date">
												<span class="date"><?=date("d",strtotime($evrow['e_date']));?></span>
												<small class="month"><?=date("M",strtotime($evrow['e_date']));?></small>
											</div>
											<img src="webimages/event/<?=$evrow['e_image'];?>" onError="this.src='webimages/imgerror.jpg'" alt="<?=$evrow['e_title'];?>">
										</div>
										<!-- event-image - end -->

										<!-- event-content - start -->
										<div class="event-content">
											<div class="event-title mb-15">
												<h3 class="title">
													<?=$evrow['e_title'];?>
												</h3>
												<span class="ticket-price yellow-color">Tickets Price ₹ <?=$evrow['e_t_price'];?></span>
											</div>
											<div class="event-post-meta ul-li-block mb-30">
												<ul>
													<li>
														<span class="icon">
															<i class="far fa-clock"></i>
														</span>
														Start <?php echo date("h:i A",strtotime($evrow['e_time_from'])); ?> - <?php echo date("h:i A",strtotime($evrow['e_time_to']));?>
													</li>
													<li>
														<span class="icon">
															<i class="fas fa-map-marker-alt"></i>
														</span>
														<?=$evrow['e_location'];?>
													</li>
												</ul>
											</div>
											<a href="event-details.php?e_id=<?=$evrow['e_id']?>" class="tickets-details-btn">
												Details
											</a>
										</div>
										<!-- event-content - end -->

									</div>
								</div>
								<!-- event-item - end -->
								<?php
								$i++;
							}?>


							<div class="col-lg-12 col-md-12 col-sm-12" style="display:none;">
								<div class="pagination ul-li clearfix">
									<ul>
										<li class="page-item prev-item">
											<a class="page-link" href="#">Prev</a>
										</li>
										<li class="page-item"><a class="page-link" href="#">01</a></li>
										<li class="page-item active"><a class="page-link" href="#">02</a></li>
										<li class="page-item"><a class="page-link" href="#">03</a></li>
										<li class="page-item"><a class="page-link" href="#">04</a></li>
										<li class="page-item"><a class="page-link" href="#">05</a></li>
										<li class="page-item next-item">
											<a class="page-link" href="#">Next</a>
										</li>
									</ul>
								</div>
							</div>

						</div>
					</div>
					<!-- conference-event - end -->

					<!-- playground-event - start -->
					<div id="playground-event" class="tab-pane fade in active show" style="display:none;">
						<div class="row">

							<?php
							$i=1;
							$sql_ev=mysqli_query($db, "Select * from cj_event inner join cj_event_category on cj_event.e_cat=cj_event_category.id where e_post_role like '%".@$_REQUEST["search"]."%' && cj_event.e_status='1' order by cj_event.mod_date DESC") or die(mysqli_error($db));
							while($evrow=mysqli_fetch_assoc($sql_ev))
							{	?>
								<!-- event-item - start -->
								<div class="col-lg-6 col-md-12 col-sm-12">
									<div class="event-item clearfix">

										<!-- event-image - start -->
										<div class="event-image">
											<div class="post-date">
												<span class="date"><?=date("d",strtotime($evrow['e_date']));?></span>
												<small class="month"><?=date("M",strtotime($evrow['e_date']));?></small>
											</div>
											<img src="webimages/event/<?=$evrow['e_image'];?>" onError="this.src='webimages/imgerror.jpg'" alt="<?=$evrow['e_title'];?>">
										</div>
										<!-- event-image - end -->

										<!-- event-content - start -->
										<div class="event-content">
											<div class="event-title mb-15">
												<h3 class="title">
													<?=$evrow['e_title'];?>
												</h3>
												<span class="ticket-price yellow-color">Tickets Price ₹ <?=$evrow['e_t_price'];?></span>
											</div>
											<div class="event-post-meta ul-li-block mb-30">
												<ul>
													<li>
														<span class="icon">
															<i class="far fa-clock"></i>
														</span>
														Start <?=$evrow['e_time_from'];?> - <?=$evrow['e_time_to'];?>
													</li>
													<li>
														<span class="icon">
															<i class="fas fa-map-marker-alt"></i>
														</span>
														<?=$evrow['e_location'];?>
													</li>
												</ul>
											</div>
											<a href="#!" class="tickets-details-btn">
												tickets & details
											</a>
										</div>
										<!-- event-content - end -->

									</div>
								</div>
								<!-- event-item - end -->
								<?php
								$i++;
							}?>

							<div class="col-lg-12 col-md-12 col-sm-12">
								<div class="pagination ul-li clearfix">
									<ul>
										<li class="page-item prev-item">
											<a class="page-link" href="#">Prev</a>
										</li>
										<li class="page-item"><a class="page-link" href="#">01</a></li>
										<li class="page-item active"><a class="page-link" href="#">02</a></li>
										<li class="page-item"><a class="page-link" href="#">03</a></li>
										<li class="page-item"><a class="page-link" href="#">04</a></li>
										<li class="page-item"><a class="page-link" href="#">05</a></li>
										<li class="page-item next-item">
											<a class="page-link" href="#">Next</a>
										</li>
									</ul>
								</div>
							</div>

						</div>
					</div>
					<!-- playground-event - end -->

					<!-- musical-event - start -->
					<div id="musical-event" class="tab-pane fade" style="display:none;">
						<div class="row">

							<?php
							$i=1;
							$sql_ev=mysqli_query($db, "Select * from cj_event inner join cj_event_category on cj_event.e_cat=cj_event_category.id where e_post_role like '%".@$_REQUEST["search"]."%' && cj_event.e_status='1' order by cj_event.mod_date DESC") or die(mysqli_error($db));
							while($evrow=mysqli_fetch_assoc($sql_ev))
							{	?>
								<!-- event-item - start -->
								<div class="col-lg-6 col-md-12 col-sm-12">
									<div class="event-item clearfix">

										<!-- event-image - start -->
										<div class="event-image">
											<div class="post-date">
												<span class="date"><?=date("d",strtotime($evrow['e_date']));?></span>
												<small class="month"><?=date("M",strtotime($evrow['e_date']));?></small>
											</div>
											<img src="webimages/event/<?=$evrow['e_image'];?>" onError="this.src='webimages/imgerror.jpg'" alt="<?=$evrow['e_title'];?>">
										</div>
										<!-- event-image - end -->

										<!-- event-content - start -->
										<div class="event-content">
											<div class="event-title mb-15">
												<h3 class="title">
													<?=$evrow['e_title'];?>
												</h3>
												<span class="ticket-price yellow-color">Tickets Price ₹ <?=$evrow['e_t_price'];?></span>
											</div>
											<div class="event-post-meta ul-li-block mb-30">
												<ul>
													<li>
														<span class="icon">
															<i class="far fa-clock"></i>
														</span>
														Start <?=$evrow['e_time_from'];?> - <?=$evrow['e_time_to'];?>
													</li>
													<li>
														<span class="icon">
															<i class="fas fa-map-marker-alt"></i>
														</span>
														<?=$evrow['e_location'];?>
													</li>
												</ul>
											</div>
											<a href="#!" class="tickets-details-btn">
												tickets & details
											</a>
										</div>
										<!-- event-content - end -->

									</div>
								</div>
								<!-- event-item - end -->
								<?php
								$i++;
							}?>

							<div class="col-lg-12 col-md-12 col-sm-12">
								<div class="pagination ul-li clearfix">
									<ul>
										<li class="page-item prev-item">
											<a class="page-link" href="#">Prev</a>
										</li>
										<li class="page-item"><a class="page-link" href="#">01</a></li>
										<li class="page-item active"><a class="page-link" href="#">02</a></li>
										<li class="page-item"><a class="page-link" href="#">03</a></li>
										<li class="page-item"><a class="page-link" href="#">04</a></li>
										<li class="page-item"><a class="page-link" href="#">05</a></li>
										<li class="page-item next-item">
											<a class="page-link" href="#">Next</a>
										</li>
									</ul>
								</div>
							</div>

						</div>
					</div>
					<!-- musical-event - end -->

					<!-- other-event - start -->
					<div id="other-event" class="tab-pane fade" style="display:none;">
						<div class="row">

							<?php
							$i=1;
							$sql_ev=mysqli_query($db, "Select * from cj_event inner join cj_event_category on cj_event.e_cat=cj_event_category.id where e_post_role like '%".@$_REQUEST["search"]."%' && cj_event.e_status='1' order by cj_event.mod_date DESC") or die(mysqli_error($db));
							while($evrow=mysqli_fetch_assoc($sql_ev))
							{	?>
								<!-- event-item - start -->
								<div class="col-lg-6 col-md-12 col-sm-12">
									<div class="event-item clearfix">

										<!-- event-image - start -->
										<div class="event-image">
											<div class="post-date">
												<span class="date"><?=date("d",strtotime($evrow['e_date']));?></span>
												<small class="month"><?=date("M",strtotime($evrow['e_date']));?></small>
											</div>
											<img src="webimages/event/<?=$evrow['e_image'];?>" onError="this.src='webimages/imgerror.jpg'" alt="<?=$evrow['e_title'];?>">
										</div>
										<!-- event-image - end -->

										<!-- event-content - start -->
										<div class="event-content">
											<div class="event-title mb-15">
												<h3 class="title">
													<?=$evrow['e_title'];?>
												</h3>
												<span class="ticket-price yellow-color">Tickets Price ₹ <?=$evrow['e_t_price'];?></span>
											</div>
											<div class="event-post-meta ul-li-block mb-30">
												<ul>
													<li>
														<span class="icon">
															<i class="far fa-clock"></i>
														</span>
														Start <?=$evrow['e_time_from'];?> - <?=$evrow['e_time_to'];?>
													</li>
													<li>
														<span class="icon">
															<i class="fas fa-map-marker-alt"></i>
														</span>
														<?=$evrow['e_location'];?>
													</li>
												</ul>
											</div>
											<a href="#!" class="tickets-details-btn">
												tickets & details
											</a>
										</div>
										<!-- event-content - end -->

									</div>
								</div>
								<!-- event-item - end -->
								<?php
								$i++;
							}?>

							<div class="col-lg-12 col-md-12 col-sm-12">
								<div class="pagination ul-li clearfix">
									<ul>
										<li class="page-item prev-item">
											<a class="page-link" href="#">Prev</a>
										</li>
										<li class="page-item"><a class="page-link" href="#">01</a></li>
										<li class="page-item active"><a class="page-link" href="#">02</a></li>
										<li class="page-item"><a class="page-link" href="#">03</a></li>
										<li class="page-item"><a class="page-link" href="#">04</a></li>
										<li class="page-item"><a class="page-link" href="#">05</a></li>
										<li class="page-item next-item">
											<a class="page-link" href="#">Next</a>
										</li>
									</ul>
								</div>
							</div>

						</div>
					</div>
					<!-- other-event - end -->

				</div>
				<!-- tab-content - end -->

			</div>
		</section>
		<!-- event-section - end
		================================================== -->





		<!-- event-gallery-section - start
		================================================== -->
		<section id="event-gallery-section" class="event-gallery-section sec-ptb-100 clearfix" style="display:none;">

			<!-- section-title - start -->
			<div class="section-title text-center mb-50">
				<small class="sub-title">harmoni gallery</small>
				<h2 class="big-title">Beautiful & <strong>Unforgettable Times</strong></h2>
			</div>
			<!-- section-title - end -->

			<div class="button-group filters-button-group mb-30">
				<button class="button is-checked" data-filter="*">
					<i class="fas fa-star"></i>
					<strong>all</strong> gallery
				</button>
				<button class="button" data-filter=".video-gallery">
					<i class="fas fa-play-circle"></i>
					<strong>video</strong> gallery
				</button>
				<button class="button" data-filter=".photo-gallery">
					<i class="far fa-image"></i>
					<strong>photo</strong> gallery
				</button>
			</div>

			<div class="grid clearfix mb-80" data-isotope="{ &quot;masonry&quot;: { &quot;columnWidth&quot;: 0 } }">
				<div class="grid-item grid-item--height2 photo-gallery " data-category="photo-gallery">
					<a class="popup-link" href="assets/images/gallery/1.image.jpg" data-rel="lightcase:photoGallery">
						<img src="assets/images/gallery/1.image.jpg" alt="Image_not_found">
					</a>
					<div class="item-content">
						<h3>John Doe Wedding day</h3>
						<span>Wedding Party, 24 June 2016</span>
					</div>
				</div>
				<div class="grid-item grid-item--width2 video-gallery " data-category="video-gallery">
					<a class="" href="https://www.youtube.com/embed/-haiaZ011OM" data-rel="lightcase:videoGallery">
						<img src="assets/images/gallery/2.image.jpg" alt="Image_not_found">
					</a>
					<div class="item-content">
						<h3>Business Conference in Dubai</h3>
						<span>Food Festival, 24 June 2016</span>
					</div>
				</div>
				<div class="grid-item photo-gallery " data-category="photo-gallery">
					<a class="popup-link" href="assets/images/gallery/3.image.jpg" data-rel="lightcase:photoGallery">
						<img src="assets/images/gallery/3.image.jpg" alt="Image_not_found">
					</a>
					<div class="item-content">
						<h3>Envato Author Fun Hiking</h3>
						<span>Food Festival, 24 June 2016</span>
					</div>
				</div>

				<div class="grid-item photo-gallery " data-category="photo-gallery">
					<a class="popup-link" href="assets/images/gallery/4.image.jpg" data-rel="lightcase:photoGallery">
						<img src="assets/images/gallery/4.image.jpg" alt="Image_not_found">
					</a>
					<div class="item-content">
						<h3>John Doe Wedding day</h3>
						<span>Wedding Party, 24 June 2016</span>
					</div>
				</div>
				<div class="grid-item grid-item--width2 video-gallery" data-category="video-gallery">
					<a class="" href="https://www.youtube.com/embed/M7nqLSwdSy4" data-rel="lightcase:videoGallery">
						<img src="assets/images/gallery/5.image.jpg" alt="Image_not_found">
					</a>
					<div class="item-content">
						<h3>New Year Celebration</h3>
						<span>Food Festival, 24 June 2016</span>
					</div>
				</div>

				<div class="grid-item grid-item--width2 photo-gallery " data-category="photo-gallery">
					<a class="popup-link" href="assets/images/gallery/6.image.jpg" data-rel="lightcase:photoGallery">
						<img src="assets/images/gallery/6.image.jpg" alt="Image_not_found">
					</a>
					<div class="item-content">
						<h3>John Doe Wedding day</h3>
						<span>Wedding Party, 24 June 2016</span>
					</div>
				</div>
				<div class="grid-item video-gallery " data-category="video-gallery">
					<a class="" href="https://www.youtube.com/embed/2vhBU0-KlNQ" data-rel="lightcase:videoGallery">
						<img src="assets/images/gallery/7.image.jpg" alt="Image_not_found">
					</a>
					<div class="item-content">
						<h3>New Year Celebration</h3>
						<span>Food Festival, 24 June 2016</span>
					</div>
				</div>
				<div class="grid-item photo-gallery " data-category="photo-gallery">
					<a class="popup-link" href="assets/images/gallery/8.image.jpg" data-rel="lightcase:photoGallery">
						<img src="assets/images/gallery/8.image.jpg" alt="Image_not_found">
					</a>
					<div class="item-content">
						<h3>Envato Author Fun Hiking</h3>
						<span>Food Festival, 24 June 2016</span>
					</div>
				</div>
			</div>

			<div class="text-center">
				<a href="#!" class="custom-btn">view all gallery</a>
			</div>


		</section>
		<!-- event-gallery-section - end
		================================================== -->





		<!-- event-expertise-section - start
		================================================== -->
		<section id="event-expertise-section" class="event-expertise-section bg-gray-light sec-ptb-100 clearfix">
			<div class="container" style="display:none;">

				<!-- section-title - start -->
				<div class="section-title text-center mb-50">
					<small class="sub-title">our services</small>
					<h2 class="big-title">harmony <strong>Expertise</strong></h2>
				</div>
				<!-- section-title - end -->

				<!-- event-expertise-carousel - start -->
				<div id="event-expertise-carousel" class="event-expertise-carousel owl-carousel owl-theme">

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img1.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">Wedding Party</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img2.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">birthday Party</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img3.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">business meeting</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img1.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">Wedding Party</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img2.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">birthday Party</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img3.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">business meeting</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img1.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">Wedding Party</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img2.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">birthday Party</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img3.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">business meeting</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img1.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">Wedding Party</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img2.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">birthday Party</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

					<!-- expertise-item - start -->
					<div class="item">
						<span class="expertise-title">harmoni party events</span>
						<div class="expertise-item">
							<div class="image image-wrapper">
								<img src="assets/images/experties/img3.jpg" alt="Image_not_found">
								<a href="#!" class="plus-effect"></a>
							</div>
							<div class="content">
								<h3 class="title">business meeting</h3>
								<p>Start from <strong>$1.200-$2.000</strong></p>
							</div>
						</div>
					</div>
					<!-- expertise-item - end -->

				</div>
				<!-- event-expertise-carousel - end -->

			</div>
		</section>
		<!-- event-expertise-section - end
		================================================== -->





		<!-- speaker-section - start
		================================================== -->
		<section id="speaker-section" class="speaker-section clearfix" style="display:none;">
			<div class="jarallax" style="background-image: url(assets/images/speaker/Black-White-Dubai-Wallpaper.jpg);">
				<div class="overlay-white">
					<div class="container">

						<!-- speaker-carousel - start -->
						<div class="speaker-carousel">
							<div class="slider-for">

								<div class="item">
									<div class="row">

										<!-- speaker-image - start -->
										<div class="col-lg-6 col-md-12 col-sm-12">
											<div class="speaker-image image-wrapper text-center">
												<img src="assets/images/speaker/speakes1.png" alt="Image_not_found">
												<span class="speaker-name"><strong>Jenni</strong> Berthas</span>
											</div>
										</div>
										<!-- speaker-image - end -->

										<!-- speaker-content - start -->
										<div class="col-lg-6 col-md-12 col-sm-12">
											<div class="speaker-content">

												<!-- section-title - start -->
												<div class="section-title text-left mb-50">
													<span class="line-style"></span>
													<small class="sub-title">Sammilan staffs</small>
													<h2 class="big-title">Professional <strong>Speakers</strong></h2>
												</div>
												<!-- section-title - end -->

												<div class="speaker-info">
													<div class="speaker-title mb-30">
														<span class="speaker-name"><strong>Jenni</strong> Berthas</span>
														<span class="work-experienc yellow-color"><strong>15 Years</strong> experienced</span>
													</div>
													<p class="black-color mb-30">
														Lorem ipsum dollor site amet the best  consectuer adipiscing elites sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam...
													</p>
													<div class="speaker-social-network ul-li">
														<h3 class="title title-medium mb-15">
															<strong>Social</strong> Network
														</h3>
														<ul>
															<li><a href="#!"><i class="fab fa-facebook-f"></i></a></li>
															<li><a href="#!"><i class="fab fa-twitter"></i></a></li>
															<li><a href="#!"><i class="fab fa-twitch"></i></a></li>
															<li><a href="#!"><i class="fab fa-google-plus-g"></i></a></li>
															<li><a href="#!"><i class="fab fa-instagram"></i></a></li>
														</ul>
													</div>
												</div>

											</div>
										</div>
										<!-- speaker-content - end -->

									</div>
								</div>

								<div class="item">
									<div class="row">

										<!-- speaker-image - start -->
										<div class="col-lg-6 col-md-12 col-sm-12">
											<div class="speaker-image image-wrapper text-center">
												<img src="assets/images/speaker/speakes1.png" alt="Image_not_found">
												<span class="speaker-name"><strong>Jonathan</strong> Doe</span>
											</div>
										</div>
										<!-- speaker-image - end -->

										<!-- speaker-content - start -->
										<div class="col-lg-6 col-md-12 col-sm-12">
											<div class="speaker-content">

												<!-- section-title - start -->
												<div class="section-title text-left mb-50">
													<span class="line-style"></span>
													<small class="sub-title">Sammilan staffs</small>
													<h2 class="big-title">Professional <strong>Speakers</strong></h2>
												</div>
												<!-- section-title - end -->

												<div class="speaker-info">
													<div class="speaker-title mb-30">
														<span class="speaker-name"><strong>Jonathan</strong> Doe</span>
														<span class="work-experienc yellow-color"><strong>15 Years</strong> experienced</span>
													</div>
													<p class="black-color mb-30">
														Lorem ipsum dollor site amet the best  consectuer adipiscing elites sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam...
													</p>
													<div class="speaker-social-network ul-li">
														<h3 class="title title-medium mb-15">
															<strong>Social</strong> Network
														</h3>
														<ul>
															<li><a href="#!"><i class="fab fa-facebook-f"></i></a></li>
															<li><a href="#!"><i class="fab fa-twitter"></i></a></li>
															<li><a href="#!"><i class="fab fa-twitch"></i></a></li>
															<li><a href="#!"><i class="fab fa-google-plus-g"></i></a></li>
															<li><a href="#!"><i class="fab fa-instagram"></i></a></li>
														</ul>
													</div>
												</div>

											</div>
										</div>
										<!-- speaker-content - end -->

									</div>
								</div>

								<div class="item">
									<div class="row">

										<!-- speaker-image - start -->
										<div class="col-lg-6 col-md-12 col-sm-12">
											<div class="speaker-image image-wrapper text-center">
												<img src="assets/images/speaker/speakes1.png" alt="Image_not_found">
												<span class="speaker-name"><strong>Denies</strong> Suarez</span>
											</div>
										</div>
										<!-- speaker-image - end -->

										<!-- speaker-content - start -->
										<div class="col-lg-6 col-md-12 col-sm-12">
											<div class="speaker-content">

												<!-- section-title - start -->
												<div class="section-title text-left mb-50">
													<span class="line-style"></span>
													<small class="sub-title">Sammilan staffs</small>
													<h2 class="big-title">Professional <strong>Speakers</strong></h2>
												</div>
												<!-- section-title - end -->

												<div class="speaker-info">
													<div class="speaker-title mb-30">
														<span class="speaker-name"><strong>Denies</strong> Suarez</span>
														<span class="work-experienc yellow-color"><strong>15 Years</strong> experienced</span>
													</div>
													<p class="black-color mb-30">
														Lorem ipsum dollor site amet the best  consectuer adipiscing elites sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam...
													</p>
													<div class="speaker-social-network ul-li">
														<h3 class="title title-medium mb-15">
															<strong>Social</strong> Network
														</h3>
														<ul>
															<li><a href="#!"><i class="fab fa-facebook-f"></i></a></li>
															<li><a href="#!"><i class="fab fa-twitter"></i></a></li>
															<li><a href="#!"><i class="fab fa-twitch"></i></a></li>
															<li><a href="#!"><i class="fab fa-google-plus-g"></i></a></li>
															<li><a href="#!"><i class="fab fa-instagram"></i></a></li>
														</ul>
													</div>
												</div>

											</div>
										</div>
										<!-- speaker-content - end -->

									</div>
								</div>

								<div class="item">
									<div class="row">

										<!-- speaker-image - start -->
										<div class="col-lg-6 col-md-12 col-sm-12">
											<div class="speaker-image image-wrapper text-center">
												<img src="assets/images/speaker/speakes1.png" alt="Image_not_found">
												<span class="speaker-name"><strong>Jonathan</strong> Doe</span>
											</div>
										</div>
										<!-- speaker-image - end -->

										<!-- speaker-content - start -->
										<div class="col-lg-6 col-md-12 col-sm-12">
											<div class="speaker-content">

												<!-- section-title - start -->
												<div class="section-title text-left mb-50">
													<span class="line-style"></span>
													<small class="sub-title">Sammilan staffs</small>
													<h2 class="big-title">Professional <strong>Speakers</strong></h2>
												</div>
												<!-- section-title - end -->

												<div class="speaker-info">
													<div class="speaker-title mb-30">
														<span class="speaker-name"><strong>Jonathan</strong> Doe</span>
														<span class="work-experienc yellow-color"><strong>15 Years</strong> experienced</span>
													</div>
													<p class="black-color mb-30">
														Lorem ipsum dollor site amet the best  consectuer adipiscing elites sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam...
													</p>
													<div class="speaker-social-network ul-li">
														<h3 class="title title-medium mb-15">
															<strong>Social</strong> Network
														</h3>
														<ul>
															<li><a href="#!"><i class="fab fa-facebook-f"></i></a></li>
															<li><a href="#!"><i class="fab fa-twitter"></i></a></li>
															<li><a href="#!"><i class="fab fa-twitch"></i></a></li>
															<li><a href="#!"><i class="fab fa-google-plus-g"></i></a></li>
															<li><a href="#!"><i class="fab fa-instagram"></i></a></li>
														</ul>
													</div>
												</div>

											</div>
										</div>
										<!-- speaker-content - end -->

									</div>
								</div>

							</div>

							<div class="slider-nav">
								<div class="item">
									<div class="item-content">
										<span class="speaker-thumbnail">
											<img src="assets/images/speaker/speakes-thumbnail.png" alt="Image_not_found">
										</span>
										<h3 class="speaker-name">Jenni Berthas</h3>
										<span class="sub-title">Sammilan Speaker</span>
									</div>
								</div>

								<div class="item">
									<div class="item-content">
										<span class="speaker-thumbnail">
											<img src="assets/images/speaker/speakes-thumbnail.png" alt="Image_not_found">
										</span>
										<h3 class="speaker-name">Jonathan Doe</h3>
										<span class="sub-title">Sammilan Speaker</span>
									</div>
								</div>

								<div class="item">
									<div class="item-content">
										<span class="speaker-thumbnail">
											<img src="assets/images/speaker/speakes-thumbnail.png" alt="Image_not_found">
										</span>
										<h3 class="speaker-name">Denies Suarez</h3>
										<span class="sub-title">Sammilan Speaker</span>
									</div>
								</div>

								<div class="item">
									<div class="item-content">
										<span class="speaker-thumbnail">
											<img src="assets/images/speaker/speakes-thumbnail.png" alt="Image_not_found">
										</span>
										<h3 class="speaker-name">Jonathan Doe</h3>
										<span class="sub-title">Sammilan Speaker</span>
									</div>
								</div>

							</div>
						</div>
						<!-- speaker-carousel - end -->

					</div>
				</div>
			</div>
		</section>
		<!-- speaker-section - end
		================================================== -->





		<!-- advertisement-section - start
		================================================== -->
		<section id="advertisement-section" class="advertisement-section clearfix" style="background-image: url(assets/images/special-offer-bg.png);">
			<div class="container">
				<div class="advertisement-content text-center">

					<h2 class="title-large white-color">Are you ready to make <strong>your Own Special Events?</strong></h2>
					<p class="mb-31">“Get started now, Sammilan event management PSD template.”</p>
					<a href="#!" class="purchase-btn">purchase now!</a>
					
				</div>
			</div>
		</section>
		<!-- advertisement-section - end
		================================================== -->





		<!-- partners-clients-section - start
		================================================== -->
		<section id="partners-clients-section" class="partners-clients-section bg-gray-light sec-ptb-100 clearfix">
			<div class="container">

				<!-- section-title - start -->
				<div class="section-title text-center mb-50">
					<small class="sub-title">we are sammilan</small>
					<h2 class="big-title">We have <strong>Best Partners & Clients</strong></h2>
					<!--p class="m-0 black-color">
						Lorem ipsum dollor site amet the best  consectuer adipiscing elites sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat insignia the consectuer adipiscing elit. 
					</p-->
				</div>
				<!-- section-title - end -->

				<div class="row">

					<!-- partners-wrapper - start -->
					<div class="col-lg-6 col-md-12 col-sm-12">
						<div class="partners-wrapper">
							<span class="carousel-title">
								Sammilan <strong>Sponsors</strong>
							</span>
							<div id="partners-carousel" class="partners-carousel owl-carousel owl-theme">
								<?php
								$query_p1 = "SELECT * FROM `cj_company` limit 6";
								$query_p2 = "SELECT * FROM `cj_company` limit 6,6";
								$query_p3 = "SELECT * FROM `cj_company` limit 12,6";
								$run_query_p1 = mysqli_query($db, $query_p1);
								$run_query_p2 = mysqli_query($db, $query_p2);
								$run_query_p3 = mysqli_query($db, $query_p3);
								if(mysqli_num_rows($run_query_p1)>0){
								?>
								<div class="item">
									<ul>
										<?php
										while($row = mysqli_fetch_array($run_query_p1))
										{
											?>
											<li style="background-color:#fff;padding:20px;">
												<img src="webimages/company/<?php echo $row['com_img'] ?>" height="60" width="100" alt="Image_not_found" onerror="this.src='webimages/profile.png'">
											</li>
											<?php
										}
										?>
									</ul>
								</div>
								<?php
								}		
								if(mysqli_num_rows($run_query_p2)>0){
								?>
								<div class="item">
									<ul>
										<?php
										while($row = mysqli_fetch_array($run_query_p2))
										{
											?>
											<li style="background-color:#fff;padding:20px;">
												<img src="webimages/company/<?php echo $row['com_img'] ?>" height="60" width="100" alt="Image_not_found" onerror="this.src='webimages/profile.png'">
											</li>
											<?php
										}
										?>
									</ul>
								</div>
								<?php
								}
								if(mysqli_num_rows($run_query_p3)>0){
								?>
								<div class="item">
									<ul>
										<?php
										while($row = mysqli_fetch_array($run_query_p3))
										{
											?>
											<li style="background-color:#fff;padding:20px;">
												<img src="webimages/company/<?php echo $row['com_img'] ?>" height="60" width="100" alt="Image_not_found" onerror="this.src='webimages/profile.png'">
											</li>
											<?php
										}
										?>
									</ul>
								</div>
								<?php
								} ?>		

							</div>
						</div>
					</div>
					<!-- partners-wrapper - end -->

					<!-- clients-testimonial - start -->
					<div class="col-lg-6 col-md-12 col-sm-12">
						<div class="clients-testimonial" style="background-image: url(assets/images/1.testimonial-bg.jpg);">
							<div class="overlay-black">

								<div class="section-title text-center mb-50">
									<small class="sub-title">testimonial</small>
									<h2 class="big-title">client <strong>says</strong></h2>
								</div>

								<div id="clients-testimonial-carousel" class="clients-testimonial-carousel owl-carousel owl-theme">
									<?php
									$query = "SELECT * FROM `cj_company`";
									$run_query = mysqli_query($db, $query);
									while($row = mysqli_fetch_array($run_query))
									{
										?>
										<div class="item text-center">
											<p class="mb-30" style="color:white;">
												"<?=html_entity_decode($row['com_desc'])?>"
											</p>
											<div class="client-info">
												<h3 class="client-name"><?=$row['com_name']?></h3>
												<span class="client-sub-title"><?=$row['com_address']?></span>
											</div>
										</div>
										<?php
									}
									?>
								</div>

							</div>
						</div>
					</div>
					<!-- clients-testimonial - end -->
					
				</div>

			</div>
		</section>
		<!-- partners-clients-section - end
		================================================== -->





		<!-- news-update-section - start
		================================================== -->
		<section id="news-update-section" class="news-update-section sec-ptb-100 clearfix">
			<div class="container">
				<div class="row">

					<!-- faq-accordion - start -->
					<div class="col-lg-6 col-md-12 col-sm-12">
						<!-- section-title - start -->
						<div class="section-title mb-30">
							<span class="line-style"></span>
							<small class="sub-title">Blogs</small>
							<?php
							$res=mysqli_query($db, "Select * from cj_blog inner join cj_event_category on cj_blog.event_category=cj_event_category.id where cj_blog.s_status='1' order by cj_blog.add_date DESC limit 1,6 ") or die(mysqli_error($db));
							?>
							<h2 class="big-title">Top <?=mysqli_num_rows($res);?> <strong>blogs</strong></h2>
						</div>
						<!-- section-title - end -->
						<div id="faq-accordion" class="faq-accordion">

							<?php
							$gh=1;
							while($resfet=mysqli_fetch_assoc($res))
							{ ?>
								<div class="card">
									<div class="card-header" id="headingone<?=$resfet['s_id'];?>">
										<button class="btn  <?=(($gh==1)?'':'collapsed')?>" data-toggle="collapse" data-target="#collapseone<?=$resfet['s_id'];?>" aria-expanded="true" aria-controls="collapseone<?=$resfet['s_id'];?>">
											<span>0<?= $gh?>.</span> <?php echo $resfet['s_name']; ?>
										</button>
									</div>

									<div id="collapseone<?=$resfet['s_id'];?>" class="collapse <?=(($gh==1)?'show':'')?>" aria-labelledby="headingone<?=$resfet['s_id'];?>" data-parent="#faq-accordion">
										<div class="card-body">
											<?php echo $resfet['s_short_desc']; ?>
											<br><br>
											<h3><a href="blog-details.php?id=<?php echo $resfet['s_id']; ?>">Read More</a></h3>
										</div>
									</div>
								</div>
								<?php $gh++;
							} ?>

						</div>
					</div>
					<!-- faq-accordion - end -->

					<!-- latest-blog-wrapper - start -->
					<div class="col-lg-6 col-md-12 col-sm-12">
						<div class="latest-blog-wrapper">

							<!-- section-title - start -->
							<div class="section-title mb-30">
								<span class="line-style"></span>
								<small class="sub-title">our blog</small>
								<h2 class="big-title">latest <strong>news</strong></h2>
							</div>
							<!-- section-title - end -->

							<!-- special-offer-section - start
							================================================== -->
							<section id="special-offer-section" class="special-offer-section clearfix" style="background-image: url(assets/images/special-offer-bg.png);">
								<div class="container">
									<div class="row">

										<!-- special-offer-content - start -->
										<div class="col-lg-11 col-md-12 col-sm-12">
											<div class="special-offer-content">
												<h2><strong>26 June 2018</strong> <span>Birthday Events</span></h2>
												<p class="m-0">
													Contact us now and we will make your event unique & unforgettable
												</p>
											</div>
										</div>
										<!-- special-offer-content - end -->

										<!-- event-makeing-btn - start -->
										<div class="col-lg-12 col-md-12 col-sm-12">
											<div class="event-makeing-btn">
												<a href="#!">View</a>
											</div>
										</div>
										<!-- event-makeing-btn - end -->

									</div>
								</div>
							</section>
							<!-- special-offer-section - end
							================================================== -->
							
							
							<!-- latest-blog - start ->
							<div class="latest-blog clearfix">
								<div class="blog-image">
									<img src="assets/images/blog/1.latest-blog.jpg" alt="Image_not_found">
									<a href="#!" class="plus-effect"></a>
								</div>
								<div class="blog-content">
									<div class="blog-title mb-30">
										<h3>Barcelona Friday Food Truck Festival 26 Mei 2019</h3>
										<span>26 June 2018</span>
									</div>
									<p class="m-0">
										Harmoni gives you everything you need to host your best event yet. lorem ipsum diamet.
									</p>
								</div>
							</div>
							<!-- latest-blog - end -->

							
						</div>
					</div>
					<!-- latest-blog-wrapper - end -->
					
				</div>
			</div>
		</section>
		<!-- news-update-section - end
		================================================== -->





		<!-- google map - start
		================================================== -->
		<section id="map-section" class="map-section clearfix" style="display:none;">
			<div class="address-wrapper" style="display:none;">
				<!-- address-info-topbar - start ->
				<div class="address-info-topbar mb-30 clearfix">
					<div class="address-info-left">
						<h3 class="title-text">Sammilan event management</h3>
						<p class="m-0">
							E-670, Pocket-3, 
							DDA Flats, 
							Bindapur Dwarka Sector-1,
							New Delhi - 110059
						</p>
					</div>

					<div class="address-info-right">
						<ul>
							<li>
								<button type="button">
									<span class="icon"><i class="fas fa-street-view"></i></span>
									<small>Direction</small>
								</button>
							</li>
							<li>
								<button type="button">
									<span class="icon"><i class="fas fa-rss"></i></span>
									<small>Save</small>
								</button>
							</li>
						</ul>
					</div>
				</div>
				<!-- address-info-topbar - end -->

				<!-- address-info-bottombar - start ->
				<div class="address-info-bottombar clearfix">
					<div class="address-info-left">
						<div class="rating-star">
							<span class="rating-point">4.5</span>
							<ul>
								<li><i class="fas fa-star"></i></li>
								<li><i class="fas fa-star"></i></li>
								<li><i class="fas fa-star"></i></li>
								<li><i class="fas fa-star"></i></li>
								<li><i class="fas fa-star-half"></i></li>
							</ul>
						</div>
						<p class="m-0">105 reviews</p>
					</div>

					<div class="address-info-right">
						<button type="button" class="map-larger-btn">
							view larger map
						</button>
					</div>
				</div>
				<!-- address-info-bottombar - end -->
					
			</div>
			<div id="google-map1">
				<div style="width: 100%"><iframe width="100%" height="600" src="https://maps.google.com/maps?width=100%&amp;height=600&amp;hl=en&amp;q=E-670%2C%20Pocket-3%2C%20DDA%20Flats%2C%20Bindapur%20Dwarka%20Sector-1+(Shinja)&amp;ie=UTF8&amp;t=&amp;z=18&amp;iwloc=A&amp;output=embed" frameborder="0" scrolling="no" marginheight="0" marginwidth="0"><a href="https://www.maps.ie/create-google-map/">Google Maps iframe generator</a></iframe></div><br />
				<!--div id="googleMaps" class="google-map-container"></div-->
			</div>
		</section>
		<!-- google map - end
		================================================== -->





		<!-- footer-section2 - start
		================================================== -->
		<footer id="footer-section" class="footer-section footer-section2 clearfix">

			<?php include"includes/footer.php";?>
			
		</footer>
		<!-- footer-section2 - end
		================================================== -->










		<!-- fraimwork - jquery include -->
		<script src="assets/js/jquery-3.3.1.min.js"></script>
		<script src="assets/js/popper.min.js"></script>
		<script src="assets/js/bootstrap.min.js"></script>

		<!-- carousel jquery include -->
		<script src="assets/js/slick.min.js"></script>
		<script src="assets/js/owl.carousel.min.js"></script>

		<!-- map jquery include -->
		<script src="assets/js/gmap3.min.js"></script>
		<script src="http://maps.google.com/maps/api/js?key=AIzaSyC61_QVqt9LAhwFdlQmsNwi5aUJy9B2SyA"></script>

		<!-- calendar jquery include -->
		<script src="assets/js/atc.min.js"></script>

		<!-- others jquery include -->
		<script src="assets/js/jquery.magnific-popup.min.js"></script>
		<script src="assets/js/isotope.pkgd.min.js"></script>
		<script src="assets/js/jarallax.min.js"></script>
		<script src="assets/js/jquery.mCustomScrollbar.concat.min.js"></script>
		<script src="assets/js/lightcase.js"></script>

		<!-- gallery img loaded - jqury include -->
		<script src="assets/js/imagesloaded.pkgd.min.js"></script>

		<!-- multy count down - jqury include -->
		<script src="assets/js/jquery.countdown.js"></script>

		<!-- color panal - jqury include -->
		<script src="assets/js/style-switcher.js"></script>

		<!-- custom jquery include -->
		<script src="assets/js/custom.js"></script>





	</body>

</html>
