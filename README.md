<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>这一天在FDU吃了什么</title>
    <style>
        :root {
            --primary: #1E88E5;
            --primary-light: #64B5F6;
            --primary-dark: #1565C0;
            --bg: #F5F9FF;
            --card-bg: #FFFFFF;
            --text: #1E2A3A;
            --text-secondary: #6B7A8C;
            --border: #DDE6F0;
            --note-color: #FF3B30;
            --note-bg: #FFF0EE;
            --note-border: #FFD4D1;
            --shadow: 0 4px 20px rgba(30, 136, 229, 0.1);
            --shadow-lg: 0 8px 40px rgba(30, 136, 229, 0.18);
            --radius: 16px;
            --radius-sm: 10px;
            --transition: 0.25s cubic-bezier(0.4, 0, 0.2, 1);
            --safe-bottom: env(safe-area-inset-bottom, 0px);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: -apple-system, 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', 'Noto Sans SC', sans-serif;
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
            padding-bottom: 100px;
            overflow-x: hidden;
            -webkit-font-smoothing: antialiased;
        }

        /* ===== 顶部导航 ===== */
        .top-bar {
            position: sticky;
            top: 0;
            z-index: 100;
            background: rgba(245, 249, 255, 0.92);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--border);
            padding: 14px 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 12px;
        }
        .top-bar .logo {
            font-size: 18px;
            font-weight: 800;
            letter-spacing: -0.5px;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 8px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .top-bar .logo .icon {
            font-size: 24px;
            flex-shrink: 0;
        }
        .top-bar .actions {
            display: flex;
            gap: 10px;
            align-items: center;
            flex-shrink: 0;
        }
        .icon-btn {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            border: none;
            background: var(--card-bg);
            cursor: pointer;
            font-size: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: var(--shadow);
            transition: var(--transition);
            color: var(--text);
            position: relative;
            user-select: none;
        }
        .icon-btn:active {
            transform: scale(0.9);
            box-shadow: 0 2px 10px rgba(30, 136, 229, 0.15);
        }

        /* ===== 日历区域 ===== */
        .calendar-container {
            max-width: 520px;
            margin: 0 auto;
            padding: 16px 16px 8px;
        }
        .calendar-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 16px;
            padding: 0 4px;
        }
        .calendar-header .month-label {
            font-size: 19px;
            font-weight: 700;
            letter-spacing: 0.3px;
            color: var(--primary-dark);
        }
        .calendar-header .nav-btns {
            display: flex;
            gap: 8px;
        }
        .calendar-header .nav-btn {
            width: 38px;
            height: 38px;
            border-radius: 50%;
            border: none;
            background: var(--card-bg);
            cursor: pointer;
            font-size: 18px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: var(--shadow);
            transition: var(--transition);
            color: var(--text);
            user-select: none;
        }
        .calendar-header .nav-btn:active {
            transform: scale(0.88);
        }
        .calendar-weekdays {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            text-align: center;
            font-size: 13px;
            font-weight: 600;
            color: var(--text-secondary);
            margin-bottom: 6px;
            padding: 0 2px;
        }
        .calendar-weekdays span {
            padding: 6px 0;
        }
        .calendar-days {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 4px;
        }
        .calendar-day {
            aspect-ratio: 1;
            border-radius: 14px;
            border: none;
            background: transparent;
            cursor: pointer;
            font-size: 15px;
            font-weight: 500;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: all 0.2s ease;
            position: relative;
            color: var(--text);
            user-select: none;
            gap: 3px;
            padding: 4px 2px;
        }
        .calendar-day:hover {
            background: #E3F2FD;
        }
        .calendar-day.other-month {
            color: #B0C4DE;
            opacity: 0.55;
        }
        .calendar-day.today {
            background: var(--primary);
            color: #fff;
            font-weight: 700;
            box-shadow: 0 4px 14px rgba(30, 136, 229, 0.35);
        }
        .calendar-day.today:hover {
            background: var(--primary-dark);
        }
        .calendar-day.selected {
            outline: 2.5px solid var(--primary);
            outline-offset: 1px;
            background: #E3F2FD;
        }
        .calendar-day.today.selected {
            outline-color: var(--primary-dark);
        }
        .calendar-day .dot {
            width: 5px;
            height: 5px;
            border-radius: 50%;
            background: var(--primary);
            flex-shrink: 0;
            transition: var(--transition);
        }
        .calendar-day.today .dot {
            background: #fff;
        }
        .calendar-day .count-badge {
            position: absolute;
            top: 3px;
            right: 5px;
            font-size: 9px;
            font-weight: 700;
            color: var(--primary);
            background: #E3F2FD;
            border-radius: 8px;
            padding: 1px 5px;
            min-width: 16px;
            text-align: center;
        }
        .calendar-day.today .count-badge {
            background: rgba(255, 255, 255, 0.35);
            color: #fff;
        }

        /* ===== 日期记录卡片 ===== */
        .day-records {
            max-width: 520px;
            margin: 0 auto;
            padding: 8px 16px 20px;
        }
        .day-records .section-title {
            font-size: 16px;
            font-weight: 700;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 0 4px;
            color: var(--primary-dark);
        }
        .record-card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 16px;
            margin-bottom: 12px;
            box-shadow: var(--shadow);
            transition: var(--transition);
            position: relative;
            overflow: hidden;
            border: 1px solid #EBF0F8;
        }
        .record-card:active {
            transform: scale(0.98);
        }
        .record-card .food-name {
            font-size: 18px;
            font-weight: 800;
            margin-bottom: 6px;
            color: var(--text);
            letter-spacing: -0.3px;
        }
        .record-card .photo {
            width: 100%;
            max-height: 260px;
            object-fit: cover;
            border-radius: var(--radius-sm);
            margin-bottom: 10px;
            background: #F5F9FF;
        }
        .record-card .tags-row {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin-bottom: 8px;
        }
        .tag {
            display: inline-flex;
            align-items: center;
            gap: 4px;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            background: #E3F2FD;
            color: var(--primary-dark);
            letter-spacing: 0.2px;
        }
        .tag.tag-canteen {
            background: #E8F5E9;
            color: #2E7D32;
        }
        .tag.tag-meal {
            background: #E3F2FD;
            color: #1565C0;
        }
        .tag.tag-portion {
            background: #FFF3E0;
            color: #E65100;
        }
        .record-card .review-text {
            font-size: 14px;
            line-height: 1.6;
            color: var(--text);
            margin-bottom: 6px;
            white-space: pre-wrap;
            word-break: break-word;
        }
        .record-card .note-box {
            background: var(--note-bg);
            border-left: 4px solid var(--note-color);
            padding: 10px 14px;
            border-radius: 0 var(--radius-sm) var(--radius-sm) 0;
            font-size: 13px;
            line-height: 1.5;
            color: #B71C1C;
            margin-top: 8px;
            display: flex;
            align-items: flex-start;
            gap: 8px;
            font-weight: 500;
        }
        .record-card .note-box .note-icon {
            font-size: 16px;
            flex-shrink: 0;
            margin-top: 1px;
        }
        .record-card .card-actions {
            position: absolute;
            top: 12px;
            right: 12px;
            display: flex;
            gap: 8px;
            opacity: 0;
            transition: var(--transition);
        }
        .record-card:hover .card-actions,
        .record-card .card-actions:focus-within {
            opacity: 1;
        }
        .record-card .action-btn {
            width: 34px;
            height: 34px;
            border-radius: 50%;
            border: none;
            background: rgba(255, 255, 255, 0.9);
            cursor: pointer;
            font-size: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
            transition: var(--transition);
            color: #E53935;
            user-select: none;
        }
        .record-card .action-btn.edit-btn {
            color: var(--primary);
        }
        .record-card .action-btn:active {
            transform: scale(0.85);
        }
        .record-card .record-time {
            font-size: 11px;
            color: var(--text-secondary);
            margin-top: 4px;
        }

        /* ===== 空状态 ===== */
        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: var(--text-secondary);
        }
        .empty-state .emoji {
            font-size: 56px;
            margin-bottom: 16px;
        }
        .empty-state .text {
            font-size: 15px;
            line-height: 1.5;
        }

        /* ===== 底部浮动加号 ===== */
        .fab {
            position: fixed;
            bottom: 28px;
            left: 50%;
            transform: translateX(-50%);
            width: 64px;
            height: 64px;
            border-radius: 50%;
            border: none;
            background: var(--primary);
            color: #fff;
            font-size: 32px;
            cursor: pointer;
            box-shadow: 0 6px 24px rgba(30, 136, 229, 0.45);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 200;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }
        .fab:active {
            transform: translateX(-50%) scale(0.88);
            box-shadow: 0 3px 12px rgba(30, 136, 229, 0.3);
            background: var(--primary-dark);
        }
        .fab .fab-icon {
            line-height: 1;
            font-weight: 300;
            margin-top: -2px;
        }

        /* ===== 模态框 ===== */
        .modal-overlay {
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.45);
            z-index: 300;
            display: none;
            align-items: flex-end;
            justify-content: center;
            backdrop-filter: blur(4px);
            -webkit-backdrop-filter: blur(4px);
            animation: fadeIn 0.2s ease;
        }
        .modal-overlay.active {
            display: flex;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        @keyframes slideUp {
            from { transform: translateY(40px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        .modal-sheet {
            background: var(--card-bg);
            border-radius: 24px 24px 0 0;
            width: 100%;
            max-width: 560px;
            max-height: 88vh;
            overflow-y: auto;
            padding: 20px 20px 30px;
            animation: slideUp 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            -webkit-overflow-scrolling: touch;
        }
        .modal-sheet .modal-handle {
            width: 40px;
            height: 4px;
            border-radius: 4px;
            background: #D0DCEB;
            margin: 0 auto 16px;
            flex-shrink: 0;
        }
        .modal-sheet .modal-title {
            font-size: 20px;
            font-weight: 800;
            margin-bottom: 18px;
            text-align: center;
            letter-spacing: -0.3px;
            color: var(--primary-dark);
        }

        /* ===== 表单 ===== */
        .form-group {
            margin-bottom: 16px;
        }
        .form-group label {
            display: block;
            font-size: 13px;
            font-weight: 700;
            color: var(--text-secondary);
            margin-bottom: 6px;
            letter-spacing: 0.3px;
            text-transform: uppercase;
        }
        .form-group label .optional {
            color: #B0A49A;
            font-weight: 500;
            text-transform: none;
            font-size: 11px;
        }
        .form-input {
            width: 100%;
            padding: 12px 16px;
            border-radius: var(--radius-sm);
            border: 1.5px solid var(--border);
            font-size: 15px;
            outline: none;
            transition: var(--transition);
            background: #FFFDFB;
            color: var(--text);
            font-family: inherit;
            resize: vertical;
            min-height: 44px;
        }
        .form-input:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(30, 136, 229, 0.12);
        }
        textarea.form-input {
            min-height: 70px;
            line-height: 1.5;
        }
        .tag-selector {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }
        .tag-option {
            padding: 8px 16px;
            border-radius: 22px;
            border: 1.5px solid var(--border);
            background: #FFFDFB;
            cursor: pointer;
            font-size: 13px;
            font-weight: 600;
            transition: all 0.2s ease;
            user-select: none;
            color: var(--text-secondary);
            font-family: inherit;
            white-space: nowrap;
        }
        .tag-option:active {
            transform: scale(0.94);
        }
        .tag-option.selected {
            background: var(--primary);
            color: #fff;
            border-color: var(--primary);
            box-shadow: 0 3px 10px rgba(30, 136, 229, 0.3);
        }
        .tag-option.tag-canteen.selected {
            background: #2E7D32;
            border-color: #2E7D32;
            box-shadow: 0 3px 10px rgba(46, 125, 50, 0.3);
        }
        .tag-option.tag-meal.selected {
            background: #1565C0;
            border-color: #1565C0;
            box-shadow: 0 3px 10px rgba(21, 101, 192, 0.3);
        }
        .tag-option.tag-portion.selected {
            background: #E65100;
            border-color: #E65100;
            box-shadow: 0 3px 10px rgba(230, 81, 0, 0.3);
        }
        .custom-input-row {
            display: flex;
            gap: 8px;
            margin-top: 8px;
        }
        .custom-input-row .form-input {
            flex: 1;
            min-height: 38px;
            padding: 8px 12px;
            font-size: 13px;
        }
        .custom-input-row .add-btn {
            padding: 8px 16px;
            border-radius: 20px;
            border: none;
            background: var(--primary-light);
            color: #fff;
            font-weight: 700;
            font-size: 13px;
            cursor: pointer;
            transition: var(--transition);
            white-space: nowrap;
            font-family: inherit;
        }
        .custom-input-row .add-btn:active {
            background: var(--primary-dark);
            transform: scale(0.95);
        }

        /* 注意部分特殊样式 */
        .note-input-wrap {
            position: relative;
        }
        .note-input-wrap .form-input {
            border-color: var(--note-border);
            background: var(--note-bg);
            color: #8B1A1A;
            font-weight: 500;
            padding-right: 40px;
        }
        .note-input-wrap .form-input::placeholder {
            color: #C89494;
            font-weight: 400;
        }
        .note-input-wrap .note-emoji {
            position: absolute;
            right: 14px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 20px;
            pointer-events: none;
        }
        .note-input-wrap .form-input:focus {
            border-color: var(--note-color);
            box-shadow: 0 0 0 3px rgba(255, 59, 48, 0.15);
        }

        /* 照片上传 */
        .photo-upload {
            border: 2px dashed var(--border);
            border-radius: var(--radius-sm);
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            background: #FFFDFB;
            position: relative;
            overflow: hidden;
            min-height: 100px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 6px;
        }
        .photo-upload:active {
            border-color: var(--primary);
            background: #F5F9FF;
        }
        .photo-upload .upload-icon {
            font-size: 32px;
            opacity: 0.6;
        }
        .photo-upload .upload-text {
            font-size: 13px;
            color: var(--text-secondary);
            font-weight: 500;
        }
        .photo-upload img.preview {
            max-width: 100%;
            max-height: 200px;
            border-radius: 8px;
            object-fit: contain;
        }
        .photo-upload .remove-photo {
            position: absolute;
            top: 8px;
            right: 8px;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            border: none;
            background: rgba(0, 0, 0, 0.55);
            color: #fff;
            cursor: pointer;
            font-size: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: var(--transition);
        }
        .photo-upload .remove-photo:active {
            transform: scale(0.85);
        }

        /* 提交按钮 */
        .submit-btn {
            width: 100%;
            padding: 16px;
            border-radius: var(--radius-sm);
            border: none;
            background: var(--primary);
            color: #fff;
            font-size: 17px;
            font-weight: 700;
            cursor: pointer;
            transition: var(--transition);
            letter-spacing: 0.5px;
            font-family: inherit;
            margin-top: 8px;
        }
        .submit-btn:active {
            background: var(--primary-dark);
            transform: scale(0.97);
        }
        .submit-btn:disabled {
            background: #D0C8C0;
            cursor: not-allowed;
            transform: none;
        }

        /* ===== 搜索页面 ===== */
        .search-panel {
            max-width: 520px;
            margin: 0 auto;
            padding: 16px 16px 20px;
        }
        .search-panel .search-input {
            width: 100%;
            padding: 14px 18px;
            border-radius: 28px;
            border: 2px solid var(--border);
            font-size: 15px;
            outline: none;
            transition: var(--transition);
            background: var(--card-bg);
            font-family: inherit;
            box-shadow: var(--shadow);
            color: var(--text);
        }
        .search-panel .search-input:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(30, 136, 229, 0.12);
        }
        .search-panel .filter-section {
            margin-top: 16px;
        }
        .search-panel .filter-section .filter-label {
            font-size: 13px;
            font-weight: 700;
            color: var(--text-secondary);
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 0.3px;
        }
        .search-panel .filter-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }
        .filter-tag {
            padding: 7px 14px;
            border-radius: 18px;
            border: 1.5px solid var(--border);
            background: var(--card-bg);
            cursor: pointer;
            font-size: 12px;
            font-weight: 600;
            transition: all 0.2s ease;
            user-select: none;
            color: var(--text-secondary);
            font-family: inherit;
        }
        .filter-tag:active {
            transform: scale(0.93);
        }
        .filter-tag.active {
            background: var(--primary);
            color: #fff;
            border-color: var(--primary);
        }
        .filter-tag.filter-canteen.active {
            background: #2E7D32;
            border-color: #2E7D32;
        }
        .filter-tag.filter-meal.active {
            background: #1565C0;
            border-color: #1565C0;
        }
        .filter-tag.filter-portion.active {
            background: #E65100;
            border-color: #E65100;
        }
        .filter-tag.filter-note.active {
            background: var(--note-color);
            border-color: var(--note-color);
        }
        .search-results-count {
            font-size: 13px;
            color: var(--text-secondary);
            margin-top: 14px;
            padding: 0 4px;
        }
        .clear-search {
            text-align: center;
            margin-top: 16px;
        }
        .clear-search button {
            padding: 10px 24px;
            border-radius: 22px;
            border: 1.5px solid var(--border);
            background: transparent;
            cursor: pointer;
            font-size: 13px;
            font-weight: 600;
            color: var(--text-secondary);
            transition: var(--transition);
            font-family: inherit;
        }
        .clear-search button:active {
            background: #E3F2FD;
            transform: scale(0.95);
        }

        /* Toast 提示 */
        .toast {
            position: fixed;
            bottom: 110px;
            left: 50%;
            transform: translateX(-50%) translateY(20px);
            background: #1E2A3A;
            color: #fff;
            padding: 12px 22px;
            border-radius: 24px;
            font-size: 14px;
            font-weight: 600;
            box-shadow: 0 6px 24px rgba(0, 0, 0, 0.25);
            opacity: 0;
            pointer-events: none;
            transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
            z-index: 500;
            white-space: nowrap;
            letter-spacing: 0.3px;
        }
        .toast.show {
            opacity: 1;
            transform: translateX(-50%) translateY(0);
        }

        /* 响应式 */
        @media (min-width: 600px) {
            .calendar-container { padding: 24px 20px 8px; }
            .day-records { padding: 12px 20px 24px; }
            .record-card { padding: 20px; }
            .modal-sheet { border-radius: 24px; margin-bottom: 20px; max-height: 80vh; }
            .modal-overlay { align-items: center; padding: 20px; }
        }
        @media (max-width: 380px) {
            .calendar-day { font-size: 13px; border-radius: 10px; }
            .calendar-day .count-badge { font-size: 8px; padding: 0 4px; }
            .top-bar .logo { font-size: 16px; }
            .record-card .card-actions { opacity: 1; }
            .record-card .action-btn { width: 30px; height: 30px; font-size: 14px; top: 8px; right: 8px; }
        }
    </style>
</head>
<body>

    <!-- 顶部导航 -->
    <header class="top-bar">
        <div class="logo">
            <span class="icon">🍜</span> 这一天在FDU吃了什么
        </div>
        <div class="actions">
            <button class="icon-btn" id="btnSearch" title="搜索" aria-label="搜索">🔍</button>
        </div>
    </header>

    <!-- 日历区域 -->
    <div class="calendar-container" id="calendarSection">
        <div class="calendar-header">
            <button class="nav-btn" id="btnPrevMonth" aria-label="上个月">◀</button>
            <span class="month-label" id="monthLabel">2024年1月</span>
            <button class="nav-btn" id="btnNextMonth" aria-label="下个月">▶</button>
        </div>
        <div class="calendar-weekdays">
            <span>日</span><span>一</span><span>二</span><span>三</span><span>四</span><span>五</span><span>六</span>
        </div>
        <div class="calendar-days" id="calendarDays"></div>
    </div>

    <!-- 日期记录 -->
    <div class="day-records" id="dayRecordsSection">
        <div class="section-title" id="recordsTitle">📅 2024年1月15日</div>
        <div id="recordsList"></div>
    </div>

    <!-- 搜索面板 -->
    <div class="search-panel" id="searchPanel" style="display:none;">
        <input type="text" class="search-input" id="searchKeyword" placeholder="🔍 搜索食物名称、评价、食堂、类型..." autocomplete="off">
        <div class="filter-section">
            <div class="filter-label">🏫 食堂名称</div>
            <div class="filter-tags" id="filterCanteens"></div>
        </div>
        <div class="filter-section">
            <div class="filter-label">🍽️ 用餐类型</div>
            <div class="filter-tags" id="filterMealTypes"></div>
        </div>
        <div class="filter-section">
            <div class="filter-label">⚖️ 分量</div>
            <div class="filter-tags" id="filterPortions"></div>
        </div>
        <div class="filter-section">
            <div class="filter-label">⚠️ 有注意标记</div>
            <div class="filter-tags" id="filterHasNote">
                <button class="filter-tag filter-note" data-value="has_note">仅看有⚠️的记录</button>
            </div>
        </div>
        <div class="search-results-count" id="searchCount"></div>
        <div id="searchResults"></div>
        <div class="clear-search">
            <button id="btnClearSearch">✕ 清除所有筛选</button>
        </div>
        <div style="text-align:center;margin-top:12px;">
            <button class="icon-btn" id="btnBackToCalendar" style="width:auto;padding:10px 24px;border-radius:22px;font-size:14px;font-weight:600;">← 返回日历</button>
        </div>
    </div>

    <!-- 底部加号按钮 -->
    <button class="fab" id="fabAdd" aria-label="添加记录">
        <span class="fab-icon">+</span>
    </button>

    <!-- 添加/编辑记录模态框 -->
    <div class="modal-overlay" id="modalOverlay">
        <div class="modal-sheet" id="modalSheet">
            <div class="modal-handle"></div>
            <div class="modal-title" id="modalTitle">🍽️ 记录今天的美味</div>

            <div class="form-group">
                <label>🍛 食物名称</label>
                <input type="text" class="form-input" id="foodNameInput" placeholder="例如：红烧肉、珍珠奶茶..." autocomplete="off">
            </div>

            <div class="form-group">
                <label>📸 照片</label>
                <div class="photo-upload" id="photoUpload">
                    <span class="upload-icon" id="uploadIcon">📷</span>
                    <span class="upload-text" id="uploadText">点击上传照片</span>
                    <img class="preview" id="photoPreview" style="display:none;" alt="预览">
                    <button class="remove-photo" id="btnRemovePhoto" style="display:none;">✕</button>
                    <input type="file" id="fileInput" accept="image/*" style="display:none;">
                </div>
            </div>

            <div class="form-group">
                <label>🏫 食堂名称</label>
                <div class="tag-selector" id="canteenSelector"></div>
                <div class="custom-input-row" id="customCanteenRow" style="display:none;">
                    <input type="text" class="form-input" id="customCanteenInput" placeholder="输入新食堂名称..." autocomplete="off">
                    <button class="add-btn" id="btnAddCustomCanteen">添加</button>
                </div>
            </div>

            <div class="form-group">
                <label>🍽️ 用餐类型</label>
                <div class="tag-selector" id="mealTypeSelector"></div>
                <div class="custom-input-row" id="customMealRow" style="display:none;">
                    <input type="text" class="form-input" id="customMealInput" placeholder="输入新用餐类型..." autocomplete="off">
                    <button class="add-btn" id="btnAddCustomMeal">添加</button>
                </div>
            </div>

            <div class="form-group">
                <label>⚖️ 分量 <span class="optional">(选填)</span></label>
                <div class="tag-selector" id="portionSelector"></div>
            </div>

            <div class="form-group">
                <label>💬 我的评价</label>
                <textarea class="form-input" id="reviewInput" placeholder="这家店的红烧肉肥而不腻，米饭有点硬..." rows="3"></textarea>
            </div>

            <div class="form-group">
                <label>⚠️ 注意 <span class="optional">(选填)</span></label>
                <div class="note-input-wrap">
                    <input type="text" class="form-input" id="noteInput" placeholder="比如：排队超长！微辣！有香菜！" autocomplete="off">
                    <span class="note-emoji">⚠️</span>
                </div>
            </div>

            <button class="submit-btn" id="btnSubmit">保存记录 ✓</button>
        </div>
    </div>

    <!-- Toast -->
    <div class="toast" id="toast"></div>

    <script>
        (function() {
            // ===== 数据存储键名 =====
            const STORAGE_KEY = 'fdu_eat_diary_v1';
            const CUSTOM_CANTEENS_KEY = 'fdu_eat_diary_canteens_v1';
            const CUSTOM_MEALS_KEY = 'fdu_eat_diary_meals_v1';

            // ===== 默认数据 =====
            const DEFAULT_CANTEENS = ['北食', '南食', '旦苑', '其他'];
            const DEFAULT_MEAL_TYPES = ['早饭', '正餐', '饮料', '甜点'];
            const DEFAULT_PORTIONS = ['量少', '正好', '量多'];

            // ===== 状态 =====
            let allData = {};
            let customCanteens = [];
            let customMealTypes = [];
            let currentYear = new Date().getFullYear();
            let currentMonth = new Date().getMonth();
            let selectedDate = formatDate(new Date());
            let isSearchMode = false;
            let selectedCanteen = null;
            let selectedMealType = null;
            let selectedPortion = null;
            let photoDataUrl = null;
            let editingRecordId = null;
            let editingDate = null;
            let activeSearchFilters = {
                canteen: null,
                mealType: null,
                portion: null,
                hasNote: false,
                keyword: ''
            };

            function formatDate(date) {
                const y = date.getFullYear();
                const m = String(date.getMonth() + 1).padStart(2, '0');
                const d = String(date.getDate()).padStart(2, '0');
                return `${y}-${m}-${d}`;
            }

            function getTodayStr() {
                return formatDate(new Date());
            }

            function generateId() {
                return Date.now().toString(36) + Math.random().toString(36).substr(2, 6);
            }

            function loadData() {
                try {
                    const raw = localStorage.getItem(STORAGE_KEY);
                    allData = raw ? JSON.parse(raw) : {};
                } catch (e) { allData = {}; }
                try {
                    const rawC = localStorage.getItem(CUSTOM_CANTEENS_KEY);
                    customCanteens = rawC ? JSON.parse(rawC) : [];
                } catch (e) { customCanteens = []; }
                try {
                    const rawM = localStorage.getItem(CUSTOM_MEALS_KEY);
                    customMealTypes = rawM ? JSON.parse(rawM) : [];
                } catch (e) { customMealTypes = []; }
            }

            function saveData() {
                try {
                    localStorage.setItem(STORAGE_KEY, JSON.stringify(allData));
                } catch (e) {
                    console.error('存储失败', e);
                    showToast('⚠️ 存储空间不足，请删除一些旧记录');
                }
                try {
                    localStorage.setItem(CUSTOM_CANTEENS_KEY, JSON.stringify(customCanteens));
                } catch (e) {}
                try {
                    localStorage.setItem(CUSTOM_MEALS_KEY, JSON.stringify(customMealTypes));
                } catch (e) {}
            }

            function getAllCanteens() {
                return [...new Set([...DEFAULT_CANTEENS, ...customCanteens])];
            }

            function getAllMealTypes() {
                return [...new Set([...DEFAULT_MEAL_TYPES, ...customMealTypes])];
            }

            function getRecordsForDate(dateStr) {
                return allData[dateStr] || [];
            }

            function getTotalRecordsCount(dateStr) {
                return getRecordsForDate(dateStr).length;
            }

            function showToast(msg) {
                const toast = document.getElementById('toast');
                toast.textContent = msg;
                toast.classList.add('show');
                clearTimeout(toast._timeout);
                toast._timeout = setTimeout(() => toast.classList.remove('show'), 2200);
            }

            function compressImage(file, callback) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = new Image();
                    img.onload = function() {
                        const canvas = document.createElement('canvas');
                        let w = img.width;
                        let h = img.height;
                        const maxW = 800;
                        const maxH = 800;
                        if (w > maxW || h > maxH) {
                            const ratio = Math.min(maxW / w, maxH / h);
                            w = Math.round(w * ratio);
                            h = Math.round(h * ratio);
                        }
                        canvas.width = w;
                        canvas.height = h;
                        const ctx = canvas.getContext('2d');
                        ctx.drawImage(img, 0, 0, w, h);
                        const dataUrl = canvas.toDataURL('image/jpeg', 0.62);
                        callback(dataUrl);
                    };
                    img.src = e.target.result;
                };
                reader.readAsDataURL(file);
            }

            function renderCalendar() {
                const monthLabel = document.getElementById('monthLabel');
                monthLabel.textContent = `${currentYear}年${currentMonth + 1}月`;

                const daysContainer = document.getElementById('calendarDays');
                daysContainer.innerHTML = '';

                const firstDay = new Date(currentYear, currentMonth, 1);
                const startWeekday = firstDay.getDay();
                const daysInMonth = new Date(currentYear, currentMonth + 1, 0).getDate();
                const daysInPrevMonth = new Date(currentYear, currentMonth, 0).getDate();
                const todayStr = getTodayStr();

                const totalCells = Math.ceil((startWeekday + daysInMonth) / 7) * 7;

                for (let i = 0; i < totalCells; i++) {
                    const dayNum = i - startWeekday + 1;
                    let displayDay;
                    let dateObj;
                    let isOtherMonth = false;

                    if (dayNum <= 0) {
                        displayDay = daysInPrevMonth + dayNum;
                        dateObj = new Date(currentYear, currentMonth - 1, displayDay);
                        isOtherMonth = true;
                    } else if (dayNum > daysInMonth) {
                        displayDay = dayNum - daysInMonth;
                        dateObj = new Date(currentYear, currentMonth + 1, displayDay);
                        isOtherMonth = true;
                    } else {
                        displayDay = dayNum;
                        dateObj = new Date(currentYear, currentMonth, displayDay);
                    }

                    const dateStr = formatDate(dateObj);
                    const isToday = dateStr === todayStr;
                    const isSelected = dateStr === selectedDate;
                    const count = getTotalRecordsCount(dateStr);

                    const btn = document.createElement('button');
                    btn.className = 'calendar-day';
                    if (isOtherMonth) btn.classList.add('other-month');
                    if (isToday) btn.classList.add('today');
                    if (isSelected) btn.classList.add('selected');
                    btn.setAttribute('data-date', dateStr);
                    btn.innerHTML = `
                        <span>${displayDay}</span>
                        ${count > 0 ? `<span class="dot"></span>` : ''}
                        ${count > 1 ? `<span class="count-badge">${count}</span>` : ''}
                    `;
                    btn.addEventListener('click', function() {
                        selectedDate = dateStr;
                        if (isOtherMonth) {
                            if (dayNum <= 0) {
                                currentMonth--;
                                if (currentMonth < 0) { currentMonth = 11; currentYear--; }
                            } else {
                                currentMonth++;
                                if (currentMonth > 11) { currentMonth = 0; currentYear++; }
                            }
                        }
                        renderCalendar();
                        renderDayRecords();
                        showCalendarSection();
                    });
                    daysContainer.appendChild(btn);
                }
            }

            function showCalendarSection() {
                isSearchMode = false;
                document.getElementById('calendarSection').style.display = 'block';
                document.getElementById('dayRecordsSection').style.display = 'block';
                document.getElementById('searchPanel').style.display = 'none';
                document.getElementById('fabAdd').style.display = 'flex';
            }

            function showSearchSection() {
                isSearchMode = true;
                document.getElementById('calendarSection').style.display = 'none';
                document.getElementById('dayRecordsSection').style.display = 'none';
                document.getElementById('searchPanel').style.display = 'block';
                document.getElementById('fabAdd').style.display = 'none';
                renderSearchFilters();
                performSearch();
            }

            function renderDayRecords() {
                const titleEl = document.getElementById('recordsTitle');
                const listEl = document.getElementById('recordsList');
                const dateObj = new Date(selectedDate + 'T00:00:00');
                titleEl.textContent = `📅 ${dateObj.getFullYear()}年${dateObj.getMonth()+1}月${dateObj.getDate()}日`;

                const records = getRecordsForDate(selectedDate);
                if (records.length === 0) {
                    listEl.innerHTML = `
                        <div class="empty-state">
                            <div class="emoji">🍽️</div>
                            <div class="text">这一天还没有记录<br>点击下方 + 号开始记录吧</div>
                        </div>
                    `;
                    return;
                }

                listEl.innerHTML = records.map((rec, idx) => {
                    const timeStr = rec.timestamp ? new Date(rec.timestamp).toLocaleTimeString('zh-CN', { hour: '2-digit', minute: '2-digit' }) : '';
                    return `
                        <div class="record-card" data-record-id="${rec.id}">
                            <div class="card-actions">
                                <button class="action-btn edit-btn" data-edit-id="${rec.id}" title="编辑">✏️</button>
                                <button class="action-btn" data-delete-id="${rec.id}" title="删除">🗑️</button>
                            </div>
                            ${rec.name ? `<div class="food-name">🍛 ${escapeHtml(rec.name)}</div>` : ''}
                            ${rec.photo ? `<img class="photo" src="${rec.photo}" alt="食物照片" loading="lazy">` : ''}
                            <div class="tags-row">
                                <span class="tag tag-canteen">🏫 ${escapeHtml(rec.canteen)}</span>
                                <span class="tag tag-meal">🍽️ ${escapeHtml(rec.mealType)}</span>
                                ${rec.portion ? `<span class="tag tag-portion">⚖️ ${escapeHtml(rec.portion)}</span>` : ''}
                            </div>
                            ${rec.review ? `<div class="review-text">${escapeHtml(rec.review)}</div>` : ''}
                            ${rec.note ? `<div class="note-box"><span class="note-icon">⚠️</span><span>${escapeHtml(rec.note)}</span></div>` : ''}
                            ${timeStr ? `<div class="record-time">🕐 ${timeStr}</div>` : ''}
                        </div>
                    `;
                }).join('');

                listEl.querySelectorAll('[data-delete-id]').forEach(btn => {
                    btn.addEventListener('click', function(e) {
                        e.stopPropagation();
                        const id = this.getAttribute('data-delete-id');
                        deleteRecord(selectedDate, id);
                    });
                });
                listEl.querySelectorAll('[data-edit-id]').forEach(btn => {
                    btn.addEventListener('click', function(e) {
                        e.stopPropagation();
                        const id = this.getAttribute('data-edit-id');
                        openEditModal(selectedDate, id);
                    });
                });
            }

            function deleteRecord(dateStr, recordId) {
                if (!confirm('确定要删除这条记录吗？')) return;
                const records = allData[dateStr] || [];
                allData[dateStr] = records.filter(r => r.id !== recordId);
                if (allData[dateStr].length === 0) {
                    delete allData[dateStr];
                }
                saveData();
                renderCalendar();
                renderDayRecords();
                showToast('🗑️ 已删除');
            }

            function escapeHtml(text) {
                const div = document.createElement('div');
                div.textContent = text;
                return div.innerHTML;
            }

            function resetForm() {
                photoDataUrl = null;
                document.getElementById('photoPreview').style.display = 'none';
                document.getElementById('uploadIcon').style.display = 'block';
                document.getElementById('uploadText').style.display = 'block';
                document.getElementById('uploadText').textContent = '点击上传照片';
                document.getElementById('btnRemovePhoto').style.display = 'none';
                document.getElementById('fileInput').value = '';
                selectedCanteen = null;
                selectedMealType = null;
                selectedPortion = null;
                document.getElementById('foodNameInput').value = '';
                document.getElementById('reviewInput').value = '';
                document.getElementById('noteInput').value = '';
                document.getElementById('customCanteenRow').style.display = 'none';
                document.getElementById('customMealRow').style.display = 'none';
                document.getElementById('customCanteenInput').value = '';
                document.getElementById('customMealInput').value = '';
                editingRecordId = null;
                editingDate = null;
                renderTagSelectors();
            }

            function renderTagSelectors() {
                const canteenSel = document.getElementById('canteenSelector');
                const allCanteens = getAllCanteens();
                canteenSel.innerHTML = allCanteens.map(c => `
                    <button class="tag-option tag-canteen ${selectedCanteen===c?'selected':''}" data-value="${escapeHtml(c)}">${escapeHtml(c)}</button>
                `).join('') + `<button class="tag-option" data-custom="canteen" style="border-style:dashed;">+ 自定义</button>`;

                const mealSel = document.getElementById('mealTypeSelector');
                const allMeals = getAllMealTypes();
                mealSel.innerHTML = allMeals.map(m => `
                    <button class="tag-option tag-meal ${selectedMealType===m?'selected':''}" data-value="${escapeHtml(m)}">${escapeHtml(m)}</button>
                `).join('') + `<button class="tag-option" data-custom="meal" style="border-style:dashed;">+ 自定义</button>`;

                const portionSel = document.getElementById('portionSelector');
                portionSel.innerHTML = DEFAULT_PORTIONS.map(p => `
                    <button class="tag-option tag-portion ${selectedPortion===p?'selected':''}" data-value="${escapeHtml(p)}">${escapeHtml(p)}</button>
                `).join('') + `<button class="tag-option" data-clear="portion" style="border-style:dotted;color:#B0A49A;">✕ 不选</button>`;

                canteenSel.querySelectorAll('.tag-option').forEach(btn => {
                    btn.addEventListener('click', function() {
                        if (this.hasAttribute('data-custom')) {
                            document.getElementById('customCanteenRow').style.display = 'flex';
                            document.getElementById('customCanteenInput').focus();
                            return;
                        }
                        selectedCanteen = this.getAttribute('data-value');
                        document.getElementById('customCanteenRow').style.display = 'none';
                        renderTagSelectors();
                    });
                });

                mealSel.querySelectorAll('.tag-option').forEach(btn => {
                    btn.addEventListener('click', function() {
                        if (this.hasAttribute('data-custom')) {
                            document.getElementById('customMealRow').style.display = 'flex';
                            document.getElementById('customMealInput').focus();
                            return;
                        }
                        selectedMealType = this.getAttribute('data-value');
                        document.getElementById('customMealRow').style.display = 'none';
                        renderTagSelectors();
                    });
                });

                portionSel.querySelectorAll('.tag-option').forEach(btn => {
                    btn.addEventListener('click', function() {
                        if (this.hasAttribute('data-clear')) {
                            selectedPortion = null;
                        } else {
                            selectedPortion = this.getAttribute('data-value');
                        }
                        renderTagSelectors();
                    });
                });
            }

            function openAddModal() {
                resetForm();
                document.getElementById('modalTitle').textContent = '🍽️ 记录今天的美味';
                document.getElementById('btnSubmit').textContent = '保存记录 ✓';
                document.getElementById('modalOverlay').classList.add('active');
                document.body.style.overflow = 'hidden';
            }

            function openEditModal(dateStr, recordId) {
                const records = allData[dateStr] || [];
                const record = records.find(r => r.id === recordId);
                if (!record) return;

                resetForm();
                editingRecordId = recordId;
                editingDate = dateStr;
                document.getElementById('modalTitle').textContent = '✏️ 编辑记录';
                document.getElementById('btnSubmit').textContent = '更新记录 ✓';

                selectedCanteen = record.canteen;
                selectedMealType = record.mealType;
                selectedPortion = record.portion || null;
                document.getElementById('foodNameInput').value = record.name || '';
                document.getElementById('reviewInput').value = record.review || '';
                document.getElementById('noteInput').value = record.note || '';

                if (record.photo) {
                    photoDataUrl = record.photo;
                    const preview = document.getElementById('photoPreview');
                    preview.src = record.photo;
                    preview.style.display = 'block';
                    document.getElementById('uploadIcon').style.display = 'none';
                    document.getElementById('uploadText').style.display = 'none';
                    document.getElementById('btnRemovePhoto').style.display = 'flex';
                }

                renderTagSelectors();
                document.getElementById('modalOverlay').classList.add('active');
                document.body.style.overflow = 'hidden';
            }

            function closeAddModal() {
                document.getElementById('modalOverlay').classList.remove('active');
                document.body.style.overflow = '';
            }

            function handleSubmit() {
                const foodName = document.getElementById('foodNameInput').value.trim();
                if (!foodName) {
                    showToast('⚠️ 请填写食物名称');
                    return;
                }
                if (!selectedCanteen) {
                    showToast('⚠️ 请选择食堂名称');
                    return;
                }
                if (!selectedMealType) {
                    showToast('⚠️ 请选择用餐类型');
                    return;
                }
                const review = document.getElementById('reviewInput').value.trim();
                const note = document.getElementById('noteInput').value.trim();

                if (editingRecordId) {
                    const records = allData[editingDate] || [];
                    const idx = records.findIndex(r => r.id === editingRecordId);
                    if (idx !== -1) {
                        records[idx] = {
                            ...records[idx],
                            name: foodName,
                            photo: photoDataUrl,
                            canteen: selectedCanteen,
                            mealType: selectedMealType,
                            portion: selectedPortion,
                            review: review,
                            note: note,
                            timestamp: records[idx].timestamp || Date.now(),
                        };
                        allData[editingDate] = records;
                        saveData();
                        closeAddModal();
                        if (editingDate === selectedDate) {
                            renderDayRecords();
                        }
                        renderCalendar();
                        showToast('✅ 记录已更新');
                    } else {
                        showToast('⚠️ 记录不存在，可能已被删除');
                    }
                } else {
                    const record = {
                        id: generateId(),
                        name: foodName,
                        photo: photoDataUrl,
                        canteen: selectedCanteen,
                        mealType: selectedMealType,
                        portion: selectedPortion,
                        review: review,
                        note: note,
                        timestamp: Date.now(),
                    };
                    const dateStr = getTodayStr();
                    if (!allData[dateStr]) {
                        allData[dateStr] = [];
                    }
                    allData[dateStr].push(record);
                    saveData();

                    selectedDate = dateStr;
                    const today = new Date();
                    currentYear = today.getFullYear();
                    currentMonth = today.getMonth();

                    closeAddModal();
                    renderCalendar();
                    renderDayRecords();
                    showCalendarSection();
                    showToast('✅ 已保存记录！');
                }
            }

            function renderSearchFilters() {
                const allCanteens = getAllCanteens();
                const allMeals = getAllMealTypes();

                const fc = document.getElementById('filterCanteens');
                fc.innerHTML = allCanteens.map(c =>
                    `<button class="filter-tag filter-canteen ${activeSearchFilters.canteen===c?'active':''}" data-value="${escapeHtml(c)}">${escapeHtml(c)}</button>`
                ).join('');

                const fm = document.getElementById('filterMealTypes');
                fm.innerHTML = allMeals.map(m =>
                    `<button class="filter-tag filter-meal ${activeSearchFilters.mealType===m?'active':''}" data-value="${escapeHtml(m)}">${escapeHtml(m)}</button>`
                ).join('');

                const fp = document.getElementById('filterPortions');
                fp.innerHTML = DEFAULT_PORTIONS.map(p =>
                    `<button class="filter-tag filter-portion ${activeSearchFilters.portion===p?'active':''}" data-value="${escapeHtml(p)}">${escapeHtml(p)}</button>`
                ).join('');

                const fhn = document.getElementById('filterHasNote');
                fhn.innerHTML =
                    `<button class="filter-tag filter-note ${activeSearchFilters.hasNote?'active':''}" data-value="has_note">⚠️ 仅看有注意的记录</button>`;

                fc.querySelectorAll('.filter-tag').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const val = this.getAttribute('data-value');
                        activeSearchFilters.canteen = activeSearchFilters.canteen === val ? null : val;
                        renderSearchFilters();
                        performSearch();
                    });
                });
                fm.querySelectorAll('.filter-tag').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const val = this.getAttribute('data-value');
                        activeSearchFilters.mealType = activeSearchFilters.mealType === val ? null : val;
                        renderSearchFilters();
                        performSearch();
                    });
                });
                fp.querySelectorAll('.filter-tag').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const val = this.getAttribute('data-value');
                        activeSearchFilters.portion = activeSearchFilters.portion === val ? null : val;
                        renderSearchFilters();
                        performSearch();
                    });
                });
                fhn.querySelectorAll('.filter-tag').forEach(btn => {
                    btn.addEventListener('click', function() {
                        activeSearchFilters.hasNote = !activeSearchFilters.hasNote;
                        renderSearchFilters();
                        performSearch();
                    });
                });
            }

            function performSearch() {
                const keyword = document.getElementById('searchKeyword').value.trim().toLowerCase();
                activeSearchFilters.keyword = keyword;

                const results = [];
                const allDates = Object.keys(allData).sort().reverse();

                for (const dateStr of allDates) {
                    const records = allData[dateStr] || [];
                    for (const rec of records) {
                        let match = true;
                        if (activeSearchFilters.canteen && rec.canteen !== activeSearchFilters.canteen) match = false;
                        if (activeSearchFilters.mealType && rec.mealType !== activeSearchFilters.mealType) match = false;
                        if (activeSearchFilters.portion && rec.portion !== activeSearchFilters.portion) match = false;
                        if (activeSearchFilters.hasNote && !rec.note) match = false;
                        if (keyword) {
                            const searchable = `${rec.name} ${rec.canteen} ${rec.mealType} ${rec.portion||''} ${rec.review} ${rec.note||''}`.toLowerCase();
                            if (!searchable.includes(keyword)) match = false;
                        }
                        if (match) {
                            results.push({ dateStr, record: rec });
                        }
                    }
                }

                const countEl = document.getElementById('searchCount');
                countEl.textContent = `找到 ${results.length} 条记录`;

                const resultsEl = document.getElementById('searchResults');
                if (results.length === 0) {
                    resultsEl.innerHTML = `
                        <div class="empty-state">
                            <div class="emoji">🔍</div>
                            <div class="text">没有找到匹配的记录<br>试试调整搜索条件吧</div>
                        </div>
                    `;
                    return;
                }

                resultsEl.innerHTML = results.map(({ dateStr, record: rec }) => {
                    const dateObj = new Date(dateStr + 'T00:00:00');
                    const dateLabel = `${dateObj.getFullYear()}年${dateObj.getMonth()+1}月${dateObj.getDate()}日`;
                    return `
                        <div class="record-card" style="margin-top:10px;">
                            <div class="record-time" style="font-size:12px;margin-bottom:6px;color:var(--primary);font-weight:600;">📅 ${dateLabel}</div>
                            ${rec.name ? `<div class="food-name">🍛 ${escapeHtml(rec.name)}</div>` : ''}
                            ${rec.photo ? `<img class="photo" src="${rec.photo}" alt="食物照片" loading="lazy" style="max-height:180px;">` : ''}
                            <div class="tags-row">
                                <span class="tag tag-canteen">🏫 ${escapeHtml(rec.canteen)}</span>
                                <span class="tag tag-meal">🍽️ ${escapeHtml(rec.mealType)}</span>
                                ${rec.portion ? `<span class="tag tag-portion">⚖️ ${escapeHtml(rec.portion)}</span>` : ''}
                            </div>
                            ${rec.review ? `<div class="review-text">${escapeHtml(rec.review)}</div>` : ''}
                            ${rec.note ? `<div class="note-box"><span class="note-icon">⚠️</span><span>${escapeHtml(rec.note)}</span></div>` : ''}
                        </div>
                    `;
                }).join('');
            }

            function initEvents() {
                document.getElementById('btnPrevMonth').addEventListener('click', function() {
                    currentMonth--;
                    if (currentMonth < 0) { currentMonth = 11; currentYear--; }
                    renderCalendar();
                });
                document.getElementById('btnNextMonth').addEventListener('click', function() {
                    currentMonth++;
                    if (currentMonth > 11) { currentMonth = 0; currentYear++; }
                    renderCalendar();
                });

                document.getElementById('btnSearch').addEventListener('click', function() {
                    if (isSearchMode) {
                        showCalendarSection();
                    } else {
                        showSearchSection();
                    }
                });

                document.getElementById('btnBackToCalendar').addEventListener('click', showCalendarSection);

                document.getElementById('btnClearSearch').addEventListener('click', function() {
                    activeSearchFilters = { canteen: null, mealType: null, portion: null, hasNote: false, keyword: '' };
                    document.getElementById('searchKeyword').value = '';
                    renderSearchFilters();
                    performSearch();
                });

                document.getElementById('searchKeyword').addEventListener('input', function() {
                    performSearch();
                });

                document.getElementById('fabAdd').addEventListener('click', openAddModal);

                document.getElementById('modalOverlay').addEventListener('click', function(e) {
                    if (e.target === this) closeAddModal();
                });

                const photoUpload = document.getElementById('photoUpload');
                const fileInput = document.getElementById('fileInput');
                photoUpload.addEventListener('click', function() {
                    fileInput.click();
                });
                fileInput.addEventListener('change', function() {
                    if (this.files && this.files[0]) {
                        const file = this.files[0];
                        if (file.size > 15 * 1024 * 1024) {
                            showToast('⚠️ 图片太大，请选择15MB以下的图片');
                            return;
                        }
                        compressImage(file, function(dataUrl) {
                            photoDataUrl = dataUrl;
                            const preview = document.getElementById('photoPreview');
                            preview.src = dataUrl;
                            preview.style.display = 'block';
                            document.getElementById('uploadIcon').style.display = 'none';
                            document.getElementById('uploadText').style.display = 'none';
                            document.getElementById('btnRemovePhoto').style.display = 'flex';
                        });
                    }
                });
                document.getElementById('btnRemovePhoto').addEventListener('click', function(e) {
                    e.stopPropagation();
                    photoDataUrl = null;
                    document.getElementById('photoPreview').style.display = 'none';
                    document.getElementById('uploadIcon').style.display = 'block';
                    document.getElementById('uploadText').style.display = 'block';
                    document.getElementById('uploadText').textContent = '点击上传照片';
                    document.getElementById('btnRemovePhoto').style.display = 'none';
                    document.getElementById('fileInput').value = '';
                });

                document.getElementById('btnAddCustomCanteen').addEventListener('click', function() {
                    const val = document.getElementById('customCanteenInput').value.trim();
                    if (!val) return;
                    if (!customCanteens.includes(val)) {
                        customCanteens.push(val);
                        saveData();
                    }
                    selectedCanteen = val;
                    document.getElementById('customCanteenRow').style.display = 'none';
                    document.getElementById('customCanteenInput').value = '';
                    renderTagSelectors();
                    showToast(`🏫 已添加「${val}」`);
                });
                document.getElementById('customCanteenInput').addEventListener('keydown', function(e) {
                    if (e.key === 'Enter') {
                        e.preventDefault();
                        document.getElementById('btnAddCustomCanteen').click();
                    }
                });

                document.getElementById('btnAddCustomMeal').addEventListener('click', function() {
                    const val = document.getElementById('customMealInput').value.trim();
                    if (!val) return;
                    if (!customMealTypes.includes(val)) {
                        customMealTypes.push(val);
                        saveData();
                    }
                    selectedMealType = val;
                    document.getElementById('customMealRow').style.display = 'none';
                    document.getElementById('customMealInput').value = '';
                    renderTagSelectors();
                    showToast(`🍽️ 已添加「${val}」`);
                });
                document.getElementById('customMealInput').addEventListener('keydown', function(e) {
                    if (e.key === 'Enter') {
                        e.preventDefault();
                        document.getElementById('btnAddCustomMeal').click();
                    }
                });

                document.getElementById('btnSubmit').addEventListener('click', handleSubmit);

                document.addEventListener('keydown', function(e) {
                    if (e.key === 'Escape') {
                        if (document.getElementById('modalOverlay').classList.contains('active')) {
                            closeAddModal();
                        } else if (isSearchMode) {
                            showCalendarSection();
                        }
                    }
                });
            }

            function init() {
                loadData();
                renderCalendar();
                renderDayRecords();
                initEvents();

                const todayStr = getTodayStr();
                if (allData[todayStr] && allData[todayStr].length > 0) {
                    selectedDate = todayStr;
                    renderCalendar();
                    renderDayRecords();
                }

                console.log('🍜 这一天在FDU吃了什么 · 已加载！');
                console.log('📅 记录日期数:', Object.keys(allData).length);
            }

            init();
        })();
    </script>
</body>
</html>
